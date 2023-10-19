# SQL-Island

SQL island is a fun way to practice SQL queries. The site can be found here: https://sql-island.informatik.uni-kl.de/ 
My completion certificate can be found attached.

[https://hyu-my.sharepoint.com/:b:/g/personal/dldntjr9517_hanyang_ac_kr/ETsRpgsIsOFOh9hksrumoA0BsKO_m8BEY937rrycZQNdzQ?e=4AooW0]

Questions and Answers 

### It seems there are a few people living in these villages. How can I see a list of all inhabitants?


SELECT * <br />
FROM inhabitant

### Thank you, Liberty! Okay, let’s see who is friendly on this island…

SELECT * <br />
FROM inhabitant<br />
WHERE state = 'friendly'

### There is no way around getting a sword for myself. I will now try to find a friendly weaponsmith to forge me one.

SELECT * <br />
FROM inhabitant<br />
WHERE state = ‘friendly’<br />
AND job = ‘weaponsmith’

### Oh, that does not look good. Maybe other friendly smiths can help you out, e.g. a blacksmith. 

SELECT * <br />
FROM inhabitant<br />
WHERE state = ‘friendly’<br />
AND job LIKE ‘%smith’

### No need to call me stranger! What’s my personid?

SELECT personid <br />
FROM INHABITANT <br />
WHERE name = ‘Stranger’

### I can offer to make you a sword for 150 gold. That’s the cheapest you will find! How much gold do you have?

SELECT gold <br />
FROM INHABITANT <br />
WHERE name = ‘Stranger’

### Damn! No mon, no fun. There has to be another option to earn gold other than going to work. Maybe I could collect ownerless items and sell them! Can I make a list of all items that don’t belong to anyone?

SELECT * <br />
FROM ITEM <br />
WHERE owner IS null

### Do you know a trick how to collect all the ownerless items?

UPDATE item <br />
SET owner = 20 <br />
WHERE owner IS NULL

Now list all of the items I have!

SELECT * <br />
FROM ITEM <br />
WHERE owner = 20

### Find a friendly inhabitant who is either a dealer or a merchant. Maybe they want to buy some of my items.

SELECT * <br />
FROM INHABITANT <br />
WHERE state = ‘friendly’ <br />
AND job = ‘dealer’ <br />
OR job = ‘merchant’

### I’d like to get the ring and the teapot. The rest is nothing but scrap. Please give me the two items. My personid is 15.

UPDATE item <br />
SET owner = 15 <br />
WHERE item = ‘ring’ <br />
OR item = ‘teapot’

### Unfortunately, that’s not enough gold to buy a sword. Seems like I do have to work after all. Maybe it’s not a bad idea to change my name from Stranger to my real name before I will apply for a job.

UPDATE inhabitant <br />
SET name = ‘Elrond’ <br />
WHERE personid = 20

### Since baking is one of my hobbies, why not find a baker who I can work for? 

SELECT * <br />
FROM inhabitant <br />
WHERE job = ‘baker’ <br />
ORDER BY gold DESC

### Is there a pilot on this island by any chance? He could fly me home.

SELECT * <br />
FROM inhabitant <br />
WHERE job = ‘pilot’

### Thanks for the hint! I can use the join to find out the chief’s name of the village Onionville. 

SELECT inhabitant.name <br />
FROM village, inhabitant <br />
WHERE village.chief = inhabitant.personid <br />
AND village.name = ‘Onionville’

### Hello Liberty, the pilot is held captive by Dirty Dieter in his sister’s house. Shall I tell you how many women there are in Onionville? Nah, you can figure it out by yourself! 

SELECT COUNT(*) <br />
FROM inhabitant, village <br />
WHERE village.villageid = inhabitant.villageid <br />
AND village.name = ‘Onionville’ <br />
AND gender = ‘f’

### Oh, only one woman. What’s her name?

SELECT name <br />
FROM inhabitant <br />
WHERE villageid = 3 <br />
AND gender = ‘f’

### Oh no, baking bread alone can’t solve my problems. If I continue working and selling items though, I could earn more gold than the worth of gold inventories of all bakers, dealers and merchants together. How much gold is that?

SELECT SUM(inhabitant.gold) <br />
FROM inhabitant <br />
WHERE job = ‘baker’ <br />
OR job = ‘dealer’ <br />
OR job = ‘merchant’

### Very interesting: For some reason, butchers own the most gold. How much gold do different inhabitants have on average, depending on their state (friendly, …)?

SELECT state, AVG(inhabitant.gold) <br />
FROM inhabitant <br />
GROUP BY state <br />
ORDER BY AVG(inhabitant.gold)

### Heeeey! Now I’m very angry! What will you do next, Liberty?

DELETE FROM inhabitant <br />
WHERE name = ‘Dirty Diane’

### Yeah! Now I release the pilot!

UPDATE inhabitant <br />
SET state = 'friendly' <br />
WHERE state = ‘kidnapped’
