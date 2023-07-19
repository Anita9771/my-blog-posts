---
title: "Building a Nostalgic 90s Birthday Invite website with HTML"
datePublished: Wed Jul 19 2023 15:32:25 GMT+0000 (Coordinated Universal Time)
cuid: clk9vtrl5000a0amnatfd08s2
slug: building-a-nostalgic-90s-birthday-invite-website-with-html
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1689780312440/efde3274-a5eb-49f9-96a2-878585745252.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1689780598233/bce05d71-a95f-4045-9483-ee2b0bc57dd3.png
tags: web-development, html5

---

# Introduction

Welcome back to our HTML for Beginners series! In my previous [article](https://annietah.hashnode.dev/building-your-first-movie-recommendation-website-with-html), we built a movie recommendation website using HTML headings, sections, and paragraph elements. We also looked at how an HTML5 file is structured. Today, we're going to embark on a journey to create a retro-90s-looking website using the list, anchor, and image elements to celebrate a special occasion—your birthday! Get ready to relive the iconic decade by building a web page that will take your guests on a nostalgic trip back in time.

In this step-by-step guide, we'll walk through the process of creating a fun-filled 90s-themed website using HTML. So, let's dive in!

## **Prerequisites**

Before we begin, make sure you have the following tools installed on your computer:

1. Visual Studio Code (VS Code): A beginner-friendly code editor that offers a comfortable environment for web development.
    
    * Download it from: [**https://code.visualstudio.com/**](https://code.visualstudio.com/)
        
2. Live Server Extension: This handy extension allows you to preview your HTML web page in real time as you make changes.
    
    * Install it from the VS Code Extensions marketplace within VS Code.
        

## Getting Started

###   
Setting the Scene

We'll create the basic structure of our website. Use the following code as a template to get you started:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>90s Retro Birthday Bash</title>
</head>
<body>
    <!-- Add your content here -->
</body>
</html>
```

### Spreading the News

  
Let your guests know what's happening! In the body section of your HTML, create a header to display the exciting birthday message:

```html
<header>
    <h1>Welcome to the 90s Retro Birthday Bash!</h1>
</header>
```

### Save the Date  

Make sure your guests mark their calendars with the date of your spectacular 90s party:

```html
<section>
    <h2>Date: July 25th, 2023</h2>
</section>
```

### Packing the Essentials  

Help your guests prepare for the ultimate 90s experience by listing the must-have items they should bring:

```html
<section>
    <h2>What to Bring:</h2>
    <ul>
        <li>Your favorite 90s outfit</li>
        <li>A mixtape of your favorite 90s songs</li>
        <li>Good vibes and dance moves</li>
    </ul>
</section>
```

### Rewinding Memories  

Add a 90s image to set the nostalgic mood:

```html
<section>
    <h2>Memories from the 90s:</h2>
    <img src="image1.jpg" alt="90s image 1">
    <!-- Add more images here if you have them -->
</section>
```

### Let's Groove  

Provide your guests with directions to the coolest 90s venue in town:

```html
<section>
    <h2>Party Location:</h2>
    <p>Come join us at the coolest 90s venue in town: <a href="https://example.com/90s-venue">The 90s Hangout</a></p>
</section>
```

### Closing Notes  

Wrap up your website with some closing notes to build anticipation for the big day:

```html
<footer>
    <p>Don't miss the fun! Let's celebrate like it's the 90s all over again!</p>
</footer>
```

The final code base should look like this:  

```xml
 <!DOCTYPE html>
 <html lang="en">
     <head>
         <meta charset="UTF-8">
         <meta name="viewport" content="width=device-width, initial-scale=1.0">
         <title>90s Retro Birthday Bash</title>
    </head>
     <body>
     <!-- Adding a header to display the birthday message -->
         <header>
             <h1>Welcome to the 90s Retro Birthday Bash!</h1>
         </header>
     <!-- Adding a section to display the date of the birthday -->
         <section>
             <h2>Date: July 25th, 2023</h2>
         </section>
     <!-- Adding a section to list what people should bring -->
         <section>
             <h2>What to Bring:</h2>
             <ul>
                 <li>Your favorite 90s outfit</li>
                 <li>A mixtape of your favorite 90s songs</li>
                 <li>Good vibes and dance moves</li>
             </ul>
         </section>
     <!-- Adding images from the 90s to create a nostalgic atmosphere -->
         <section>
             <h2>Memories from the 90s:</h2>
             <img src="image1.jpg" alt="90s image 1">
         <!-- Add more images here if you have them -->
         </section>
     <!-- Adding an anchor tag to show the location of the party -->
         <section>
             <h2>Party Location:</h2>
             <p>Come join us at the coolest 90s venue in town:
                 <a href="https://example.com/90s-venue">The 90s Hangout</a>
             </p>
         </section>
     <!-- Adding a footer with some closing notes -->
         <footer>
             <p>Don't miss the fun! Let's celebrate like it's the 90s all over again!</p>
         </footer>
     </body>
</html>
```

With the image below as output:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1689780210915/fb454332-cef9-4842-8365-2964c1850fe0.png align="center")

# Conclusion

  
There you have it! With the power of HTML, you've created an awesome 90s-themed website to announce and celebrate your birthday in style. The best part is, you've done it all on your own! Now, your guests will be thrilled to join you on this nostalgic journey.