![Cover Image](./cover-image.jpg)

*photo by [@sincerelymedia](https://unsplash.com/@sincerelymedia)*

# Creating a Portfolio Website Using GitHub Pages and React: Part 3

**Part 1 on why I chose GitHub Pages and React is available [here](https://dev.to/ionabrabender/creating-a-portfolio-website-using-github-pages-and-react-part-1-1mm4).**
<br>
**Part 2 on how to get started with your GitHub Pages and React app is available [here](https://dev.to/ionabrabender/creating-a-portfolio-website-using-github-pages-and-react-part-2-16e1).**

As a recent software engineering graduate, I decided to create a portfolio website as a way to showcase what I can do as well as to improve my coding skills. In previous posts, I've discussed [why GitHub Pages and React are good tools for a portfolio site](https://dev.to/ionabrabender/creating-a-portfolio-website-using-github-pages-and-react-part-1-1mm4) and [how to get started with your app](https://dev.to/ionabrabender/creating-a-portfolio-website-using-github-pages-and-react-part-2-16e1). **In this post I'll be looking at how I set up my custom domain and added it to my GitHub Pages and React website.** While a custom domain name is completely optional, it can be a great way to personalise your portfolio.

**Click [here](https://ionabrabender.com/) to see the website I've created using GitHub Pages and React.**

<br></br>
***
<br></br>

## Why Use a Custom Domain?

When you [create your GitHub Pages website](https://dev.to/ionabrabender/creating-a-portfolio-website-using-github-pages-and-react-part-2-16e1), it will automatically be published at your equivalent of username.github.io (in this case, mine would be iona-b.github.io). While it's absolutely fine to use this URL, there are a couple of reasons why you might want to consider using a custom domain.

### 1. It Can Help You Strengthen Your Brand

When you originally created your GitHub account, you may have chosen a username that's not completely recognisable as you. While you can [change your username](https://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-your-github-user-account/changing-your-github-username), there might be unintended side effects, so it's something you may want to avoid. You can mitigate this issue by choosing a custom domain name that makes your site immediately identifiable to visitors and minimises any potential confusion.

### 2. It Makes Your Website Look More Professional

Using the github.io version doesn't look bad by any means, but having your own custom domain shows that you're taking your portfolio website seriously and that you have the skills to properly configure it.

### 3. It Can Be Free or Relatively Inexpensive

Most domain registrars offer your first domain registration at a relatively low price and some will even give you a certain period for free. You should look carefully at the terms before signing up to avoid any hidden costs, but getting your personalised domain name is a no-brainer if you can find a good deal.

## How to Use a Custom Domain Name with a GitHub Pages and React Website

To use a custom domain with your GitHub Pages and React website, follow these steps:

### 1. Decide on a Domain Name

Generally, when it comes to choosing a domain name for a portfolio website, the firstnamelastname.com format is preferred, as it makes your site easy to find. If someone else has already registered your preferred domain name, try to come up with a close alternative (perhaps you can add a dash between your first and last name, or include a middle name?) and make sure that you're consistent across all of your online branding. If you've already established a personal brand using something other than the firstname + lastname format, go with that.

### 2. Choose a Domain Registrar

There are many companies with which you can register a domain name and they'll often offer additional services, such as a sizeable storage limit or a backup system. Some factors you may want to consider include pricing, expiration policies, whether you can transfer a domain name to another registrar, add ons and hidden fees, and other users' reviews. You can find an overview of some of the most highly-rated registrars [here](https://hostingfacts.com/domain-registrars/), so make sure you look around and consider all of your options before deciding.

### 3. Set up Your Domain Name System (DNS)

The [Domain Name System (DNS)](https://www.cloudflare.com/learning/dns/what-is-dns/) is a naming system for computers and other resources connected to the internet and is responsible for translating domain names to IP addresses, which in turn allows your browser to load the resources at that IP address.

Once you've registered your domain, it's likely that you'll need to set it up correctly to be able to use it. As I used [GoDaddy](https://www.godaddy.com/offers/brand/repeat?isc=goodbr01&gclid=CjwKCAjw_sn8BRBrEiwAnUGJDqZz7ciO66I91q57s-7fVxRyhhGnnjm08IBfArEepTcUNbdbRNvJiRoC2_wQAvD_BwE&gclsrc=aw.ds) for my domain name, I'll be explaining specifically how to configure your DNS settings using this service. If you've chosen a different domain registrar, you may need to search for instructions specific to that service, however the rest of this guide should still be relevant.

#### **Configuring Your DNS Settings Using GoDaddy.com**
Go to the DNS Management Page for your chosen domain and make the following changes:

1. In the Type A row, update the value to 185.199.108.153. This allows your domain name to point to the GitHub server.
2. Add another Type A row and use the IP address value of 185.199.109.153.
3. Add another Type A row and use the IP address value of 185.199.110.153.
4. Add another Type A row and use the IP address value of 185.199.111.153.
5. Add your GitHub Pages URL as the value for the Type CNAME row. For me, this would be iona-b.github.io.

Once you've made those changes, your finalised DNS Management page should look something like this:

![Updated DNS Management Page](./dns-management.png)

*Updated DNS Management Page*

### 4. Add Your Domain Name to Your App

Once you've correctly configured your DNS settings, go to the package.json file for your app. When you initially set this up, you probably added your version of ```"homepage": "http://iona-b.github.io/"``` to the first section of the file. You can now update this with your new domain name. It should end up looking something like this:

![Add Domain Name to package.json](./add-domain-name-to-package-json.png)

*Add Domain Name to package.json*

Make sure you push your changes and run ```npm run deploy``` before moving onto the next step.

### 5. Add Your Domain Name to Your Repository

Finally, you just need to add your domain name to your repository. Go to the GitHub Pages section of your repo and add your new domain name to the Custom Domain Section and save. The updated page should look like this: 

![Add Domain Name to GitHub Repository](./add-custom-domain-to-github-pages.png)

*Add Domain Name to GitHub Repository*

And that's it! You should now be able to access your website at your custom URL.

<br></br>
***
<br></br>

In the next post, I'll be looking more at the React app itself and how we can use it to create an effective portfolio website. See you then!

**Part 1 on why I chose GitHub Pages and React is available [here](https://dev.to/ionabrabender/creating-a-portfolio-website-using-github-pages-and-react-part-1-1mm4).**
<br>
**Part 2 on how to get started with your GitHub Pages and React app is available [here](https://dev.to/ionabrabender/creating-a-portfolio-website-using-github-pages-and-react-part-2-16e1).**

## Sources
1. "[Configuring a custom domain for your GitHub Pages site](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/configuring-a-custom-domain-for-your-github-pages-site)", GitHub Docs, Accessed October 23, 2020
2. "[Changing your GitHub username
](hhttps://docs.github.com/en/free-pro-team@latest/github/setting-up-and-managing-your-github-user-account/changing-your-github-username)", GitHub Docs, Accessed October 23, 2020
3. "[GoDaddy Domain with GitHub Pages](https://medium.com/@JinnaBalu/godaddy-domain-with-github-pages-62aed906d4ef)", Jinna Balu on Medium, Accessed October 23, 2020
4. "[10 Best Domain Registrars](https://hostingfacts.com/domain-registrars/)", HostingFacts, Accessed October 23, 2020
5. "[What is DNS?](https://www.cloudflare.com/learning/dns/what-is-dns/)", Cloudflare, Accessed October 23, 2020