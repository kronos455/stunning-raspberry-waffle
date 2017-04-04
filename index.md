# Placeholder for my 'How-to' Raspberry Pi 3 Bramble

## Preface
This page explains how I put together the Raspberry Pi 3 Bramble. Because I didn't know any Linux command line when I first started, this 
recipe may sound condescendingly basic for anyone with basic Linux skills. However, I really want to keep the recipe as simple as possible to allow the most number of interested people to be able to replicate what I've done. 

Let me know of any typos or anything else you feel this recipe is missing. This document might be a work-in-progress for a little while. I'm open to constructive criticism. I'll put some pics in as well at a later date. I realize that this page, as is, is as bland as toast.

## Components

--> Raspberry PI 3 B's: I used 4. I've seen clusters built with as few as 2. The sky's the limit if you want to do more. I also refer to these as 'RP3B' because typing more than I have to seem inefficient.
Sources: http://www.microcenter.com/product/460968/Raspberry_Pi_3_Model_B, http://amzn.to/2oFOKu4

--> USB Power Source: I used a 5-port power source. Just make sure your power source is a minimum of 2.5 amps per port (the power source sold seperately for the RP3B is 5 amp). More on this later. 
Sources: http://amzn.to/2ozrd1h

--> A router: I used a basic, 5-port router to start. It was cheap. Then I was invited present the cluster to some folks at the university I attend for my Master's and I needed a wireless to make the cluster remotely. It's up to you. 
Sources: (wired) http://amzn.to/2oGa02T, (wireless) http://amzn.to/2oFQ5kF

--> 32 GB Micro SD cards: I had 4 Raspberry PI's so I bought 4 Micro SD Cards. You can go small or big on the disk volume, depending on your intended use, however, I would HIGHLY recommend Class 10 or above if possible. The higher the class, the faster the read & write speeds. I noticed that the Class 10's were significantly faster than the Class 4's I started out with. 
Sources: http://amzn.to/2oA7LBh

--> Micro USB cables: You'll need 4. I liked the flat ones. Makes it easy to aesthetically manage the cables. 
Sources: http://amzn.to/2oznxwD

--> Ethernet Patch Cables: You'll need 4. These are flat, too. 
Sources: http://amzn.to/2oFYCnW

--> Electrical Strip: Need one to plug in your power source and router. Out of caution, I bought one that had some surge protection and an accompanying guarantee. They are a little more expensive but they make you feel like you're protecting your newly acquired toy during a thunder-storm. 
Sources: http://amzn.to/2ozuI7J

--> USB Fan: Just for fun. 
Sources: http://amzn.to/2oFYHb2

--> Acrylic, Stacked Case: Gives a nice presentation of the cluster. 
Sources: http://amzn.to/2ozuIEN

This is how I assembled the cluster. Feel free to get artistic. Just keep in mind that there are certain thing that you can't change - each RP3B absolutely needs 2.5 amps or more power, etc. And this isn't an endorsement of Amazon but they do make things easier.

## Citing Sources

I did not make this cluster in a vacuum. I don't have the technical background necessary to "wing it". However, with the right instruction just about anyone can get started and learn. I had no background in Linux so it took me about a month to get the cluster working the first time.

Beginner Linux code: 

http://www.makeuseof.com/tag/15-useful-commands-every-raspberry-pi-user-should-know/

Begin here for Hadoop: 

http://www.widriksson.com/raspberry-pi-hadoop-cluster/#The_setup

http://www.widriksson.com/raspberry-pi-2-hadoop-2-cluster/#Clear_HDFS_filesystem

http://arturmkrtchyan.com/how-to-setup-multi-node-hadoop-2-yarn-cluster

https://developer.ibm.com/recipes/tutorials/building-a-hadoop-cluster-with-raspberry-pi/

https://robcnamahoe.wordpress.com/2016/12/06/setting-up-hadoop-on-a-raspberry-pi-cluster/



## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/kronos455/stunning-raspberry-waffle/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/kronos455/stunning-raspberry-waffle/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
