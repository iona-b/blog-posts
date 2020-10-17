![Cover Image](./cover-image.jpg)

*photo by [@lum3n](https://unsplash.com/@lum3n)*

# Creating a Portfolio Website Using GitHub Pages and React: Part 2

**Read part 1 [here](https://dev.to/ionabrabender/creating-a-portfolio-website-using-github-pages-and-react-part-1-1mm4).**

In this series of blog posts, I'll be talking about why and how I created my portfolio website using GitHub Pages and React.

**Click [here](ionabrabender.com) to see the website I've created using GitHub Pages and React.**

<br></br>
***
<br></br>

## Step 1: Getting Set Up

If you're at the stage where you've decided to create your portfolio website using GitHub Pages and React, it's likely that you already have a good setup in terms of what you need to get started. In any case, we'll quickly go over what you'll need.

### 1. A GitHub Account
You can sign up for a free GitHub account at [github.com](https://github.com/).

### 2. Install Git on Your Machine
Git often comes pre-installed as standard with most operating systems, but you can check by running ```git version``` in the terminal and seeing if it returns a version number. If you don't have it installed, you can find a comprehensive guide for GitHub Desktop, MacOS, Windows, and Linux users [here](https://github.com/git-guides/install-git).

### 3. Set Up GitHub Correctly
Once you have your GitHub account set up and have installed Git on your computer, you'll need to make sure you've configured everything correctly and have added your SSH key to your account. You can find a comprehensive guide for Mac users [here](http://burnedpixel.com/blog/setting-up-git-and-github-on-your-mac/) and for Windows users [here](https://medium.com/@aklson_DS/how-to-properly-setup-your-github-repository-mac-version-3a8047b899e5).

### 4. Install Node.js and NPM
Briefly, Node.js is a JavaScript runtime environment and is used to execute programs written using JavaScript. You can find an overview [here](https://www.freecodecamp.org/news/what-exactly-is-node-js-ae36e97449f5/). npm is works as a software library, a package manager, and an installer. It's open-source, contains almost 1 million packages, and is a great way for developers to share code. Click [here](https://www.w3schools.com/whatis/whatis_npm.asp) for more information. You can download Node.js from the official website [here](https://nodejs.org/en/).

### 5. Select Your Text Editor
You'll need to have a text editor installed in order to edit your code. I really like using Visual Studio Code (available to download [here](https://code.visualstudio.com/)), but you're free to use whatever you're most comfortable with.

## Step 2: Creating Your GitHub Repository
The next step is to set up the repository which will contain your website files. After logging into your GitHub account, click the button to [create a new repository](https://github.com/new). In order for GitHub Pages to work correctly, you'll need to name this repository like so: <username>.github.io, where the username is your **exact** GitHub username.

** Image **

So, mine would be iona-b.github.io.

## Step 3: Creating Your Initial React App
At this point, we won't be creating a fully-functioning React app. We just want to get to the stage where we can get your site online.

<br></br>

To initialise your React app, cd into whichever directory you want to work in and run ```npm init react-app <whatever-you-want-to-name-your-app>```. 

## Step 4. Install GitHub Pages as a Dev-Dependency

In order for your site to work, you'll need to install [gh-pages](https://www.npmjs.com/package/gh-pages), which you can do by cd-ing into your React app and running ```npm install gh-pages --save-dev```.

## Step 5: Update Your package.json File
When you initialise your React app, you'll notice that a package.json file is automatically generated for you. This is a JSON file that is used to manage the project's dependencies, scripts, and versions. To make sure your website can deploy properly, there are three lines of code we'll need to add.

### 1. Add a Home Page
In the first section of the package.json file, add a homepage, for instance: ```"homepage": "http://iona-b.github.io/"```.

### 2. Add Predeploy
In the scripts section, add a predeploy, for instance: ```"predeploy": "npm run build"```

### 3. Add Deploy
Also in the scripts section, add a deploy, like so: ```"deploy": "gh-pages -d build"```

Your additions should look something like this:

<br></br>

![Cover Image](./package-json.png)

<br></br>

## Step 6: Push to GitHub

Once you've completed the above steps, it's time to get your React site online! To do so, you can run the following commands:

```
git init
git commit -m "first commit"
git branch -M main
git remote add origin <repository URL>
git push -u origin main
```

## Step 7: Deploy

Simply run ```npm run deploy``` and the script you added to your package.json file should kick into action.

## Step 8: Update Your Repository Settings

Go to settings in your repository and look at the GitHub Pages section. Underneath the Source heading, you should have the option to select which branch the sit is being built from. Change the branch to gh-pages. This way, your repository will know what you want to use to build your website.

## Step 9: Celebrate Your New Website
Sure, you don't actually have anything on it at this point, but you've done the hard work and now you can start on the fun part of personalising your portfolio website!

![Celebration Image](./celebration-image.jpg)

*photo by [@amyshamblen](https://unsplash.com/@amyshamblen)*


<br></br>
***
<br></br>

In future posts, I'll be working through exactly how I built my website using GitHub Pages and React. See you then!


## Sources
1. "[About GitHub Pages](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/about-github-pages)", GitHub Docs, Accessed October 8 2020
2. "[Setting up a GitHub Pages site with Jekyll
](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/setting-up-a-github-pages-site-with-jekyll)", GitHubDocs, Accessed October 8 2020
3. "[What is GitHub Pages](https://pages.github.com/)", GitHub Pages, Accessed October 8 2020

https://guides.github.com/features/pages/