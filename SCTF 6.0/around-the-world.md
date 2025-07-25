# Around the World
## Disclaimer: I did not solve this challenge in time, and required quite a substantial amount of hints to finish it.

Category: **OSINT**  
Difficulty: **Hard (Tedious)**

Before we start, we have a message from the challenge setter on how I solved this challenge:
<img width="100%" height="auto" alt="Screenshot 2025-07-22 at 08 17 14" src="https://github.com/user-attachments/assets/4c591c93-9731-4688-be87-f1a6431f4ed3" />

I cannot agree enough.  
Not only did this challenge take me through the 10 stages of hell, it might have also taken me through the 5 stages of grief. Nonetheless, let's get into how we solved it after countless hours.

## Stage 1: Limbo
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

A simple google search (or chatgpt search, whatever floats your boat) revealed this to be a type of text to text steganography using Zero-Width Characters. Using [this website](https://330k.github.io/misc_tools/unicode_steganography.html), we decode the message pretty easily.
<img width="1680" height="452" alt="Screenshot 2025-07-22 at 20 40 09" src="https://github.com/user-attachments/assets/dc8ce6bf-7ed5-431a-847a-f122269546fc" />
We get two hidden texts: ```Archive.ph``` and ```https://tinyurl.com/3p6vurwj```

Hooray! We've gotten past the first stage! **9 more to go...**  

## Stage 2: Lust

The Second Circle of Hell (Lust), was described to blow souls about in a violent storm. That's exactly how I felt, doing this next stage.

The ```archive.ph``` didn't really interest me, but the tinyurl link did. Clicking into it brings us to an Instagram page:
<img width="1126" height="724" alt="Screenshot 2025-07-25 at 12 05 55" src="https://github.com/user-attachments/assets/4b663420-298e-4565-a2d5-cadc11e43e32" />
The bio explicitly told us the ```archive.ph``` was not working, so that's great, which means we skip a step!

Hooray.

Anyway, looking into it, we see three Instagram posts, each with its own caption.  
However, none of them led you anywhere, except to locations. At this point, I was speculating we might need to return to this point later in the question, but with no hints, I was unable to think of anything.

I kid you not, I was stuck on this particular section for an hour, hoping maybe the coordinates spelt out something.








##### for later steps


Let's take a look at the posts a bit closer, from the latest to the most recent.
### Post 1: The mysterious event
<img width="1106" height="702" alt="Screenshot 2025-07-25 at 12 11 48" src="https://github.com/user-attachments/assets/ef97a4a1-5ef6-4b48-9fd6-4548c2aa6932" />

<img width="1109" height="705" alt="Screenshot 2025-07-25 at 12 12 42" src="https://github.com/user-attachments/assets/53a0319c-0d89-4f69-bcf9-33b7ddb53239" />

The caption said:
> The event was amazing!! Though I should now figure out a way over to where my hotel is…








