# Around the World
## Disclaimer: I did not solve this challenge in time, and required quite a substantial amount of hints to finish it.

Category: **OSINT**  
Difficulty: **Hard (Tedious)**

Before we start, we have a message from the challenge setter on how I solved this challenge:
<img width="100%" height="auto" alt="Screenshot 2025-07-22 at 08 17 14" src="https://github.com/user-attachments/assets/4c591c93-9731-4688-be87-f1a6431f4ed3" />

I cannot agree enough.  
Not only did this challenge take me through the 10 stages of hell, it might have also taken me through the 5 stages of grief. Nonetheless, let's get into how we solved it after countless hours.

## Stage 1: Diary.txt
At the start of the challenge, we are given the file ```diary.txt``` along with the caption: 
> I had a dream, a dream of travelling around the world. I’ve spent years planning to ensure that when I embark on my trip, it’s going to be perfect. I’ll be starting on my trip in a few more months. I’m so excited!

At first glance, we aren't given many clues on what we are supposed to find, nor even how the flag would be formed.  
Since no coordinates were mentioned, I ruled out a simple Google image search, as most setters would tell us how many decimal places the flag would require.  

The next step I took was to open the ```diary.txt```, using my text editor (The default one on a MacBook).  
At first glance, nothing seemed out of the ordinary, just a diary message about how this person wanted to travel the world.  
<img width="1468" height="900" alt="Screenshot 2025-07-22 at 20 18 24" src="https://github.com/user-attachments/assets/efda73f7-f42b-4e88-8b36-db421cc03319" />

I proceeded to then spend the next half hour crashing out over this, figuring something was wrong with my computer. This stage of the challenge literally made me feel in limbo, in a situation where I seemed to be caught between two stages, and it was unclear what would happen next.

Out of desperation, I decided to look at the text file from a different angle. I opened my terminal and did the command ```strings diary.txt```, used to find the printable strings in a file.  

I noticed something really strange about the text, it was broken up in a really weird way that made no sense to me. If this was a normal plaintext, why was it broken up randomly?  
<img width="555" height="698" alt="Screenshot 2025-07-22 at 20 26 22" src="https://github.com/user-attachments/assets/569789cf-76cd-4f88-948d-0ff7e7c90dbe" />

Therefore, I decided to do ```cat -v diary.txt``` to display non-printing characters so they are visible.
<img width="1446" height="351" alt="Screenshot 2025-07-22 at 20 29 19" src="https://github.com/user-attachments/assets/5c10e5a0-8265-4842-a318-0774f197108d" />

Doing this revealed a ton of non-printing characters that were hiding in between the text.

**What is steganography doing in my OSINT?????** I exclaimed, but I had no choice but to continue.  

A simple Google search (or ChatGPT search, whatever floats your boat) revealed this to be a type of text-to-text steganography using Zero-Width Characters. Using [this website](https://330k.github.io/misc_tools/unicode_steganography.html), we decode the message pretty easily.
<img width="1680" height="452" alt="Screenshot 2025-07-22 at 20 40 09" src="https://github.com/user-attachments/assets/dc8ce6bf-7ed5-431a-847a-f122269546fc" />
We get two hidden texts: ```Archive.ph``` and ```https://tinyurl.com/3p6vurwj```

Hooray! We've gotten past the first stage! **9 more to go...**  

## Stage 2: GitHub

The ```archive.ph``` didn't really interest me, but the tinyurl link did. Clicking into it brings us to an Instagram page:
<img width="1126" height="724" alt="Screenshot 2025-07-25 at 12 05 55" src="https://github.com/user-attachments/assets/4b663420-298e-4565-a2d5-cadc11e43e32" />
The bio explicitly told us the ```archive.ph``` was not working, so that's great, which means we skip a step!

Hooray.

Anyway, looking into it, we see three Instagram posts, each with its own caption.  
However, none of them led you anywhere, except to locations. At this point, I was speculating we might need to return to this point later in the question, but with no hints, I was unable to think of anything.

I kid you not, I was stuck on this particular section for an hour, hoping maybe the coordinates spelt out something.

I figured there might be other sites we need to check, and one of the more common websites to check is GitHub.

Github usernames don't accept full-stops in their usernames, though, so I removed the full-stop to search the username ```theoj02```, which popped up this user:
<img width="1423" height="860" alt="Screenshot 2025-07-30 at 08 21 52" src="https://github.com/user-attachments/assets/68521e66-7816-4f5e-b220-abfcc8a6eee1" />

Seems like we found the right user.

The biography of the user states:
> I've left traces of planning for my trip both here and somewhere else online, do provide me with some advice if you could!

But I couldn't find anything on GitHub, and the repository ```botbot``` didn't really have anything, with the repository being a bot to store routes that the user wanted to take on his trip around the world.

However, additional information about commits can be found through GitHub's API, so we went to the only commit this person has made:
<img width="1418" height="863" alt="Screenshot 2025-07-30 at 08 25 43" src="https://github.com/user-attachments/assets/cdda7d41-5b4e-43d2-9c46-8e2f22f637ee" />

And added a ```.patch``` behind the url to get additional information.
<img width="1280" height="808" alt="Screenshot 2025-07-30 at 08 26 35" src="https://github.com/user-attachments/assets/1b57b1d6-d8d1-4b4a-92b3-65142182efc4" />

This reveals the user's email, ```sctf2025@gmail.com```


## Stage 3: Gmail + Google Calender

The easiest way to find more information and data from a Gmail account comes from a Google-specific OSINT Framework called ```ghunt```.
It's able to find information linked to gmail account.

Using the command ```ghunt email sctf2025@gmail.com```, we are able to find the following information:
<img width="774" height="858" alt="Screenshot 2025-07-30 at 08 32 50" src="https://github.com/user-attachments/assets/f2ed566d-b39f-4eab-864d-747f3ffdebe2" />

We found a public Google Calendar that we can download, and it looks like it has information about a World Tour. Given that this is a gmail account probably specifically created for this OSINT, we can safely assume that there is additional information in this calender.

Downloading it shows you these few planned events:
<img width="909" height="469" alt="Screenshot 2025-07-30 at 08 34 38" src="https://github.com/user-attachments/assets/d75a2641-62f7-439a-873a-6999c4669aa7" />

Each event has a location, but a very strange string of numbers is hidden as the description of one of the events:
<img width="514" height="238" alt="Screenshot 2025-07-30 at 08 35 32" src="https://github.com/user-attachments/assets/a238b4a7-e0a0-411d-8d75-c44c8e0833ad" />

The number looks like an ID of sorts, and I tried x.com first, but hit a dead end as the link was invalid.

After digging for a while, I discovered that it could also be a Discord Snowflake ID, so i used an online [Guild Lookup website](https://discordlookup.com/guild/) and found this Discord Server:
<img width="996" height="482" alt="Screenshot 2025-07-30 at 08 41 46" src="https://github.com/user-attachments/assets/9d536c37-582c-4c34-a592-ce31cb4695ba" />
Seems legitimate enough...


## Stage 4: Discord
Clicking the Instant Invite URL actually brings you to the server, in which you discover you have access to a bot called ```travel bot```.




##### for later steps


Let's take a look at the posts a bit closer, from the latest to the most recent.
### Post 1: The mysterious event
<img width="1106" height="702" alt="Screenshot 2025-07-25 at 12 11 48" src="https://github.com/user-attachments/assets/ef97a4a1-5ef6-4b48-9fd6-4548c2aa6932" />

<img width="1109" height="705" alt="Screenshot 2025-07-25 at 12 12 42" src="https://github.com/user-attachments/assets/53a0319c-0d89-4f69-bcf9-33b7ddb53239" />

The caption said:
> The event was amazing!! Though I should now figure out a way over to where my hotel is…








