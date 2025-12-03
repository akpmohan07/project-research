https://chatgpt.com/c/69309d89-68d4-8325-a39c-c4a9554b6d4e

# Symbol-Based URL Sharing — Project Summary

## Why I'm Doing This
This whole idea started in my college library. There was a Christmas tree where everyone could write something positive on a note and hang it. While writing mine, I thought about sharing my website—but writing a full URL looked out of place on such a warm, handwritten note. A QR code also felt too techy and visually noisy for that environment.

That moment made me wonder:
**Can I share my website in a simple, handwritten, creative way—something subtle, personal, and interesting?**

I wanted something that blends naturally with a handwritten message but still lets curious people reach my site. That’s where this symbol-based sequence idea came from.

---

## What I Explored and Discussed
### 1. The general concept
I looked into whether there are existing websites or platforms that let me turn a handwritten pattern or sequence into a URL, kind of like a human-writable QR code. It turns out nothing mainstream does this, which pushed me into brainstorming alternatives.

### 2. Brainstorming ways to encode URLs without QR codes
I explored:
- simple symbol sequences  
- geometric shapes  
- tic-tac-toe style 3×3 grids  
- personal logos and signatures  
- human-readable codes  
- AI recognition concepts  
- pattern-to-URL mappings  

The goal was to find something easy to draw, easy to understand, and visually fitting for handwritten notes.

### 3. Scenarios where this can be used
I looked at different use cases including:
- handwritten notes  
- presentations  
- treasure-hunt style experiences  
- low-tech spaces  
- personal messages  
- creative or aesthetic communication  
- private but discoverable link sharing  

These all helped shape the idea.

### 4. Security considerations
I evaluated how secure this kind of system could be. Key points:
- QR codes embed data directly, making them hard to guess.
- Symbol sequences rely on a lookup system, so security depends on design.
- Using 4 shapes in a 3×3 grid gives 262,144 combinations.
- I can add rate-limits or expiry if needed.
- This is not meant for sensitive content, but it is fine for public or semi-public use.

### 5. Choosing the method
I compared three main approaches:
1. A custom personal symbol  
2. Using my autograph as the key  
3. A 3×3 grid filled with 4 simple shapes  

After comparing aesthetics, complexity, and usability, I decided the **4-shape 3×3 grid** is the most practical and visually pleasing for what I’m doing.

### 6. Implementation plan
I outlined a simple way to build the system without AI:
- Pick 4 hand-drawn shapes (like ● ▲ ■ ★).
- Create my own 3×3 pattern.
- Write that pattern on my Christmas note.
- Build a webpage where users manually recreate the pattern.
- If the pattern matches, they get redirected to my website.

This works with basic HTML, CSS, and JavaScript—no scan, no AI, nothing fancy.

---

## Final Thoughts
The entire point of this project is to create a **warm, handwritten, creative way** to share my website that fits the vibe of a personal message. Instead of a QR code or a long URL, I’m designing a tiny visual puzzle that curious people can try.

It’s personal.
It’s aesthetic.
It’s simple.
And it actually fits the environment where I had the idea.

