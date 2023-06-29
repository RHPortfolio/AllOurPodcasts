To run locally, try `bundle exec jekyll serve `


1. How to update the seasons wiki 

Update the sheets doc with the right data in the YAML sheet. Remember
- use `" "` around film names and episode numbers
- separate films by commas and write them all out in one cell

Copy and paste the data up to 'films' into this xls to YAML converter
[you can find it here](https://tableconvert.com/excel-to-yaml).

Then use YAML Validator to paste in the YAML markdown, test it for errors and format it to work easiest with jekyll
[you can find it here](https://jsonformatter.org/yaml-validator).


To update the film database, prior to pushing content, run the following command locally:
`ruby film.rb`

This script loads all existing data from films-tmdb.yml and seasons-wiki.yml, and checks if there are any films listed in the latter which don't exist in the former; anything missing is then searched for using the tmdb database, and the content is stored for later retrieval (including film metadata and artwork)




# How to Add A Podcast Feed

## Choose a codename
This is a variable almost that is used in a number of settings. Pick it now and be consistent. Preferablly use a single word or initialism without punctuation or you may end up with problems. e.g. "thispodcast"

## Define a data file
Make sure there is a .yml file in the `\_data` folder.

Within this, you need to define the following:

- podcast_title: the title of the podcast as you want it to appear in feeds. Write this as a string, for example `"`"This Podcast"`
- podcast_url: the url on the website that the podcast will be available for browsing, in the form `/podcasts/thispodcast` 
- podcast_feed_url: point to where in this project the xml template is listed, in the form `/thispodcast.xml`
- podcast_album_art: point to the location of the image as hosted in the local project. This should be in the form `/ßassets/1400x1400_This-Podcast.jpg`
- podcast_owner: the name of the owner of the podcast. This will be displayed in podcast metadata through the . This shoudl be a string, for example `"This Podcast Productions (Jimmy Newpod)"`
- podcast_email: the email for the podcast to be contacted through. This is displayed in podcast metadata, but also stands as a point of contact some services use for authenticating you. It should be a string, such as `"info@thispodcast.com"`
- podcast_category: this is a simple category tag, but they are dictated by iTunes. You can find the list of available categories on [this website](https://podcasters.apple.com/support/1691-apple-podcasts-categories). This should appear as a string, e.g. `"Leisure"`
- podcast_subcategory_one: you can list two subcategories, again [using standardised subcategories from itunes](https://podcasters.apple.com/support/1691-apple-podcasts-categories). This should appear like this: `"Hobbies"`
- podcast_subcategory_two: And again, e.g. `"Animation & Manga"`
- podcast_explicit: simple string response which can be either "yes", "no", or "clean", which is expressed in podcast feed metadata and allows filtering in podcast libraries such as iTunes. Write as a string, e.g. `"yes"`
- podcast_author: The author of the podcast. `"Me3 Comedy"`
- description: some room to provide a podcast `"All of our podcasts consolidated into a single feed"`
- podcast_summary: e.g. `"All of our podcasts consolidated into a single feed"`
- podcast_subtitle: e.g. bm,.:"{po`"Listen, it'll be alright"`

## Add folder for containing episodes
 Under 'podcasts' in the site architecture, you need to add a folder to collect all relevant episodes. Episodes are 'published' by a single markdown file in the relevant feed's parent folder.

 For simplicity's sake, use a single word or uninterrupted initialism for the folder name, preceded by an underscore, e.g. This Podcast's folder `/_tp`

## Adding an Episode
In the appropriate podcast folder, add a markdown file, with the title beginning with a date. Date format should be
`YYYY-MM-DD` followed by an all lowercase kebabcase filename describing the episode. Be consistent with titling as it helps with admin.

## List podcast in Podcasts data file

## Add podcast to Config.yml
Note when editing a yml file that indents and spaces are integral to the language.

### Add Podcast to 'Collections'
Simple really. Under collections add a hyphon with the codename you use for the podcast e.g. thispodcast (note, no speech marks required - consider this a variable name not a string).

In the second 'collections' heading, list the podcast in the following format: 
`	thispodcast:
		output: true`

This ensures the feed is supposed to be published.

### Add defaults
This ensures all the necessary fields have values. These can be overwritten. It's messy, I should remove this, or remove other listings. 

### Restart Project
The config file is only run at build, so you'll need to restart your development server or force a new build for these changes to take effect - but this should ensure things go live...

## Create an xml feed file
Name it simply, e.g. `podcast-name.xml`

Then copy and paste the following.

`
---
layout: null	
---
{% include podcast.xml ext="mp3" podcast=site.data.dataSource episodes=site.episodeSource %}```

You need to change what podcast points to, and which episodes to draw from. Usually these will be the same name you have set as the podcast folder name and the data file without any punctuation.

What this file does is borrow from teh template file which is podcast.xml. In that, it lays out the fundamentals of an rss feed. If you have trouble with validating your feed, it is likely that they can be fixed by digging in that. This only renders on build, so don't expect the podcast feed to update without pushing changes to the site. `

## Create a Podcast page
This is the landing page for your podcast. It should be in the root folder, and be named *codeword*.md

In it, you should include the following to use a podcast page template, and provide the following information:

`
---
layout: podcast
title: Seasons
permalink: /podcasts/seasons
collection: "seasons"
podcast: "seasons"
id: "seasons"
---

Seasons podcast.
{{page.layout}}
{{page.title}}
{{page.permalink}}
{{page.collection}}

`

