To run locally, try `bundle exec jekyll serve `


1. How to update the seasons wiki 

Update the sheets doc with the right data in the YAML sheet. Remember
- use `" "` around film names and episode numbers
- separate films by commas and write them all out in one cell

Copy and paste the data up to 'films' into this xls to YAML converter
[https://tableconvert.com/excel-to-yaml](you can find it here)

Then use YAML Validator to paste in the YAML markdown, test it for errors and format it to work easiest with jekyll



To update the film database, prior to pushing content, run the following command locally:
`ruby film.rb`

This script loads all existing data from films-tmdb.yml and seasons-wiki.yml, and checks if there are any films listed in the latter which don't exist in the former; anything missing is then searched for using the tmdb database, and the content is stored for later retrieval (including film metadata and artwork)