# #theGamificationProject

### 🎮 Play with Friends & Family

- Hold friendly competitions with your loved ones on personal improvement;
- Be the first to know when they accomplish wins in their lives;
- Help each other out when you are stuck on your growth journey.

## 🎮 Top Players 🎮

[Gamification Leaderboard (AK)](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Gamification%20Leaderboard%20(AK)%20c5d85b7b8197480bba533671d19a8b14.md)

---

## 📅 Get Work Done

---

**How to use:** Earn rewards as you accomplish wins; track deadlines, punctuality, and progress on your wins.

[Success Plan](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Success%20Plan%2090ed258452e34298b83734ddb01c7df4.md)

### ✔️ Hand in your Quests!

---

**How to use: Hand in your quests by dragging and dropping items from above into `Wins Today`!**

[Success Plan](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Success%20Plan%2092b2622d2ed24334b26b096b760010db.md)

## 🧘‍♀️ Build Strong Habits

---

**How to use:** Leverage scarcity to motivate you to complete daily habits; track daily progression.

[Daily Quests](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Daily%20Quests%20fbcff1bb204d46fcacdba1a948747ead.md)

### 🕓 Earn Your Leisure Time

- Ever felt guilty for watching that extra 30 mins of TV or cheating on your diet?
- Well, be guilty no more - legitimately earn gold to spend towards your 'unproductive' moments.
- Adaptive to any leisure activities you do.

## 🤑 Spend Your Gold

---

[Item Shop](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Item%20Shop%205e063cc8d77f4826bcd22862e4e832b3.md)

You can pick your rewards and spend gold in your daily quests in the property `Reward Purchased?`

---

## Initialization: What's Your Name?

---

Let's personalize the system for you, shall we?

---

- Modify the below directly to fit your needs.
    
     Please update your name everywhere you see **Your Avatar (YA).** You can also add your own custom cover images to personalize your avatar!
    
    [Gamification Leaderboard (AK)](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Gamification%20Leaderboard%20(AK)%20e8cfa0058cf34d5f9320a47f09c5f431.md)
    
    Let's also change anything with YA to your initials.
    
    [Gamification Tags](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Gamification%20Tags%20a372610afce74031a05daafe18aae9a4.md)
    

# Upgrade Your Look!

---

> Gamification is most fun when you're fully immersed into your fantasy world! Browse our theme library for inspiration. Share your theme [here](https://notion.conradlin.com/Co-x3-Shared-Gamification-Page-ca3f2e9589d54562afc3c9b6071f54e4#16b1688524cc4303ba5989ad4cd570f3)!
> 

[https://youtu.be/963WNVhQFsk](https://youtu.be/963WNVhQFsk)

[Co-x3 Theme Library](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Co-x3%20Theme%20Library%203a5e715a711c468395874892bc707b51.md)

# Your Customization Options

---

![#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/screencapture-notion-so-conradlin-Vanilla-Dashboard-c229dffcb649494d9f64bb9e814b0800-2020-07-05-02_24_42.png](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/screencapture-notion-so-conradlin-Vanilla-Dashboard-c229dffcb649494d9f64bb9e814b0800-2020-07-05-02_24_42.png)

[Fantasy World Theme](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Fantasy%20World%20Theme%2015717ce3890047e6ab1ea9aad9755cf3.md)

![#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/screencapture-notion-so-conradlin-Fantasy-World-Theme-5186cf9c909f4968889181a86b8ea780-2020-07-04-23_23_57.png](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/screencapture-notion-so-conradlin-Fantasy-World-Theme-5186cf9c909f4968889181a86b8ea780-2020-07-04-23_23_57.png)

---

## Code Documentation

---

[Success Plan](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Success%20Plan%20c303e08eb78742cf9f254202f5f947bc.md)

- **Success Plan 🏆**
    
    ---
    
    `Multiplier` checks if the quest is complete, then add the difficulty number + the punctuality as a multiplier to how much experience you should earn for the quest.
    
    ```jsx
    if(equal(prop("Status"), "Complete"), prop("Difficulty #") + prop("+/-"), 0)
    ```
    
    `Difficulty Number` checks if the quest is complete, and then if the difficulty level is empty (you did not pick how difficult this quest will be), defaults to 1, otherwise, translate it to a number. This property is rolled up to the gamification tags database to help calculate how much gold reward you should earn for this quest.
    
    ```jsx
    if(equal(prop("Status"), "Complete"), if(empty(prop("Difficulty Level?")), 1, toNumber(prop("Difficulty Level?"))), 0)
    ```
    
    `+/-` checks for the difference between the do date and the closing date, multiplies by a factor (0.05 in my situation), and then by the difficulty number. In layman's terms, what I am calculating here is, depending on how many days early or late you are in completing this task, we are multiplying by a factor to make the adjustment smaller, and then multiplying by the difficulty level so that the effort needed on the quest is accounted for when adjusting the rewards based on punctuality.
    
    ```jsx
    dateBetween(prop("Do Date"), prop("Closing Date"), "days") * 0.05 * prop("Difficulty #")
    ```
    
    `Punctuality` is a view property (for information only) that checks for the difference between the "Do Date" and the "Closing Date", and returns how many days early or late you have completed the quest (or on time!).
    
    ```jsx
    (not empty(prop("Do Date"))) ? (empty(prop("Closing Date")) ? if(toNumber(dateBetween(end(prop("Do Date")), now(), "days")) == 0 and not now() < end(prop("Do Date")), "⚠ Finish Today!", if(now() > end(prop("Do Date")), "🚨 Late " + format(abs(toNumber(dateBetween(end(prop("Do Date")), now(), "days")))) + " day(s)!", "⏱ " + format(toNumber(dateBetween(end(prop("Do Date")), now(), "days") + 1)) + " day(s) to go!")) : if(prop("Closing Date") == end(prop("Do Date")), "✔️ On Time!", if(prop("Closing Date") > end(prop("Do Date")), "🚨 Late " + format(abs(toNumber(dateBetween(end(prop("Do Date")), prop("Closing Date"), "days")))) + " day(s)!", "⭐ Early " + format(toNumber(dateBetween(end(prop("Do Date")), prop("Closing Date"), "days"))) + " day(s)!"))) : "⚠ No Target"
    ```
    

[Daily Quests](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Daily%20Quests%20c631710dbbb14716b7ae46208b8b549e.md)

- **Daily Quests 🕐**
    
    ---
    
    `Multiplier` checks which habits have been done for the day (toNumber basically translates the ✅ into binary (1 or 0), and also checks if the text property Eat Breakfast is filled out (to also show 1 or 0). The result is that we will get a sum of 1s or 0s that will tell us exactly how many daily quests have been done for the day! When you want to add more daily quests (properties) to your tracker, you will need to also add the corresponding value as an addition item inside this formula.
    
    ```jsx
    toNumber(prop("🧘‍♂️ Meditate")) + ((not empty(prop("🍳 Eat Breakfast"))) ? 1 : 0) + toNumber(prop("⏩ Today's 5")) + toNumber(prop("💪🏼 Exercise")) + toNumber(prop("✍🏻 Write")) + toNumber(prop("📚 Learn Somthing New"))
    ```
    
    `Completion %` divides the # of habits completed today by the # of habits you have defined to be completed every day. Then, we multiply by 100 to get the %, and round it to make sure it is a whole number. Remember to change the `# of habits` property if and when you add or remove habits to do.
    
    ```jsx
    round(prop("Multiplier") / prop("# of Habits") * 100)
    ```
    
    `Difficulty #` checks if the completion % is over 70% (which is my first milestone) then output 1, otherwise if 100% completion, output 2. This rolls up into gamification tags to determine how much gold reward you should earn for completing these quests.
    
    ```jsx
    if(largerEq(prop("Completion %"), 70), if(equal(prop("Completion %"), 100), 2, 1), 0)
    ```
    
    `Progress Bar` converts the completion % into a progress bar. 
    
    ```jsx
    (prop("Multiplier") / prop("# of Habits") >= 1) ? "✅" : format(slice("■■■■■■■■■■", 0, floor(prop("Multiplier") / prop("# of Habits") * 10)) + format(slice("□□□□□□□□□□", 0, ceil(10 - prop("Multiplier") / prop("# of Habits") * 10)) + " " + format(round(prop("Multiplier") / prop("# of Habits") * 100)) + (empty(prop("Multiplier")) ? "%" : "%")))
    ```
    

[Gamification Tags](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Gamification%20Tags%200d87d57a25a04a88be9d5fe1f26005c6.md)

- **Gamification Tags 🏷**
    
    ---
    
    `Total EXP` adds the EXP multipler (rolled up) from both Success Plan and Daily Quests, multiplying by the `Base EXP` that you can define and adjust.
    
    ```jsx
    (prop("YA: Success Plan (EXP Multiplier)") + prop("YA: Daily Quests (EXP Multiplier)")) * prop("Base EXP")
    ```
    
    `Total Gold` checks if the checkbox `Gold?` is ✅, then add the Difficulty Gold Bounty (rolled up) from both Success Plan and Daily Quests, multiplying by the `Base Gold` that you can define and adjust.
    
    ```jsx
    prop("Gold?") ? (prop("YA: Success Plan (Difficulty Gold Bounty)") + prop("YA: Daily Quests (Difficulty Gold Bounty)")) * prop("Base Gold") : 0
    ```
    
    **If you want to add new users, you will need to do 2 things.** 
    
    1. Add new tags as rows to signify 25 min or 5 min tasks. 
    2. Relate their success plan and daily quests into the gamification tags database. Roll up the multipler and difficulty # for both.
    3. Inside total EXP and total gold, you will also need to add in the rollups for their respective EXP Multipliers and Difficulty Gold Bounty

[Gamification Leaderboard (AK)](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Gamification%20Leaderboard%20(AK)%2005e408ea9a07461ab40d93e31e1f62d4.md)

- **Gamification Leaderboard 🏋️‍♂️**
    
    ---
    
    The formulas for the suffix (Title) here are mainly utilized to present information for visually by adding labels to content. 
    
    `Level #` checks if EXP earned is not 0, then have the experience earned divided by the EXP to level.
    
    ```jsx
    (prop("EXP Earned") != 0) ? floor(prop("EXP Earned") / prop("EXP to Level")) : 0
    ```
    
    `EXP to next level` multiplies the EXP to level * the current level + 1 subtracting the EXP earned already to calculate how much EXP you need to level up.
    
    ```jsx
    round(prop("EXP to Level") * (prop("Level #") + 1) - prop("EXP Earned"))
    ```
    
    `Level Up Bar` converts EXP earned into a progress bar
    
    ```jsx
    ((prop("EXP to Level") - prop("EXP to Next Level")) / prop("EXP to Level") >= 1) ? "✅" : format(slice("■■■■■■■■■■", 0, floor((prop("EXP to Level") - prop("EXP to Next Level")) / prop("EXP to Level") * 10)) + format(slice("□□□□□□□□□□", 0, ceil(10 - (prop("EXP to Level") - prop("EXP to Next Level")) / prop("EXP to Level") * 10)) + " " + format(round((prop("EXP to Level") - prop("EXP to Next Level")) / prop("EXP to Level") * 100)) + (empty(prop("EXP to Next Level")) ? "%" : "%")))
    ```
    

[Item Shop](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/Item%20Shop%206a5b4a79189b496b92dc81d6489715ed.md)

- **Item Shop 💰**
    
    ---
    
    `YA Gold Spend` multiplies the # of times purchases by the costs.
    
    ```jsx
    prop("YA # Of Times Purchased") * prop("Costs")
    ```
    
    `Total Gold Spend` This is where you add gold spends for additional gold spend by other characters!
    
    ```jsx
    prop("YA Gold Spend")
    ```
    

# Theory & Resources

---

### 🎮 [Best Practices On How To Gamify Your Productivity](https://www.notion.so/316e34a2a23148638fac63f8f5627db0)

## Overview

---

[https://youtu.be/Lc7UJMeEY6w](https://youtu.be/Lc7UJMeEY6w)

## Comprehensive Guide (Must Watch!)

---

[https://www.youtube.com/watch?v=8G6K8H9uLxE](https://www.youtube.com/watch?v=8G6K8H9uLxE)

## Gamification Theory

---

[https://youtu.be/yBM5KDPlLQ0](https://youtu.be/yBM5KDPlLQ0)

# Why Struggle Alone?

Now that you've successfully gamified your life, join the Co-x3 Community and post your weekly character progression in the leaderboard space! It's a space is built for members who desire that extra bit of accountability, motivation, and congratulations from a supportive community.

1. [Join the community - it's free!](http://co-x3.com)
2. Read this [article](https://x3.conradlin.com/posts/lets-gamify-our-lives) to understand what we're trying to accomplish
3. [Post your update and support others on their growth journey](https://x3.conradlin.com/groups/2140488/topics/2140501)

## Support Us! 💕

<aside>
🐤 [**Share about us on social media**](https://twitter.com/intent/tweet?url=https%3A%2F%2Fgamify.conradlin.com&text=Check%20out%20this%20amazing%20project%20that%20turns%20your%20life%20into%20a%20RPG%21&hashtags=theGamificationProject)

</aside>

<aside>
🧰 **[Check out more templates](http://notion.co-x3.com)**

</aside>

<aside>
🗺️ **[Contribute to the roadmap](https://www.notion.so/7432bac67d6c4c328d4fe59b724dbb58)**

</aside>

<aside>
🌟 **[Explore the enhanced version](https://www.notion.so/ffe9a03aff1542cd8ad394e61fee0b4a)**

</aside>

![#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/SupportiveCommunity.png](#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/SupportiveCommunity.png)

# Share your Experience

---

[https://conradlin.typeform.com/to/M23vGm](https://conradlin.typeform.com/to/M23vGm)

## Get in Touch! 👋

---

A collaborative project by [Conrad Lin](http://conradlin.com). All Rights Reserved.

***#theGamificationProject** was initialized due to the starking realization that we are rarely in control of our own lives. This fact is made abundantly clear when attempting mindful meditation - simply focusing on your breath for minutes at a time seems like an impossible task for many new practitioners. Every day, our brain continuously spins wild tales of reality to make sense of the world around us - sometimes for the better, and at times for the worse. Gamification for good, to drive productivity, is my attempt to create a sustainable structure in which the human brain is self-motivated to accomplish much more in less time.* 

---

<aside>
<img src="#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/favicon.png" alt="#theGamificationProject%20e7d1a2891b604089968b4f8ea8feb0f5/favicon.png" width="40px" /> **[Website](http://www.conradlin.com)**

</aside>

<aside>
<img src="https://cdn2.iconfinder.com/data/icons/social-media-2285/512/1_Twitter_colored_svg-512.png" alt="https://cdn2.iconfinder.com/data/icons/social-media-2285/512/1_Twitter_colored_svg-512.png" width="40px" /> [**Twitter**](https://twitter.com/cryptolin)

</aside>

<aside>
✉️ [**Email Me**](mailto:lets.talk@conradlin.com)

</aside>

<aside>
<img src="data:image/png;base64,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" alt="data:image/png;base64,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" width="40px" /> [**Youtube**](https://www.youtube.com/c/ConradLin)

</aside>

<aside>
<img src="data:image/png;base64,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" alt="data:image/png;base64,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" width="40px" /> [**LinkedIn**](https://www.linkedin.com/in/conradlin/)

</aside>

<aside>
💌 [**Subscribe**](https://www.conradlin.com/subscribe/)

</aside>

# Want More? 💭

## If you need more help and resources, please find some useful links below.

**Be Intentional**

[FAQ](https://x3.conradlin.com/posts/faq-be-intentional) · [Playlist](https://www.youtube.com/watch?v=57jZikDOI60&list=PLgDMbYMf0e_r6ddiipAwrZ1UqLCGJhx55) · [Course](http://learn.co-x3.com)

**Make Work Fun**

[FAQ](https://www.guilded.gg/thex3family/groups/Gza4RWEd/channels/210f1d9d-1f66-47dc-af71-f8f874a2d921/forums) · [Playlist](https://www.youtube.com/watch?v=yBM5KDPlLQ0&list=PLgDMbYMf0e_qQcwhhhNuIYtAfOnodFzzC) · [Course](https://toolbox.co-x3.com/LVL-UP)

<aside>
🚀 [**Power Up Today →**](https://conradl.in/4b21d)

</aside>

[https://chilipepper.io/form/wild-diced-fresnos-85ca0bd2-3de8-43d3-8141-68c92068d1b9](https://chilipepper.io/form/wild-diced-fresnos-85ca0bd2-3de8-43d3-8141-68c92068d1b9)