# Website of Synqs based on Wowchemy

- [**Get Started**](https://wowchemy.com/templates/)
- [Hugo Academic CLI](https://github.com/wowchemy/hugo-academic-cli/):** Automatically import publications from BibTeX

# Howto update my profile
- Your profile lives in 'content/authors/YOUR-NAME'
- If you just would like to change some details you might open the 'content/authors/YOUR-NAME/_index.md' file it on the github website, edit it and that should be about it.

## Bigger work on your profile

If you would like to create a new user and do bigger changes it might be best to install github desktop first and clone this repository.

- Download github desktop [here](https://desktop.github.com/).
- Clone this repository,  whose URL is https://github.com/synqs/synqs.github.io
- Change the file/create the folder in `content/authors/YOUR-NAME`.
- Follow here the examples of the other profiles that were previously created.
- `Push` or `create a pull request` if you have no admin rights.

## Add a Talk/Poster

If you would like to add your talk/poster to the website it might be best to install github desktop first and clone this repository.

- Download github desktop [here](https://desktop.github.com/).
- Clone this repository,  whose URL is https://github.com/synqs/synqs.github.io
- Change the create the folder in `content/talk/YEAR-NAME-EVENT`.
- The folder should contain the following:
    - a pdf of your talk/poster
    - an png/jpg image representing your talk/poster
    - an index file giving some key details
- Follow here the examples of the other posters/talks that were previously created.
- `Push` or `create a pull request` if you have no admin rights.

## Quick fixes with weird bugs during building

Sometimes you have weird bugs in your local build. You can just test if you can get rid of them by cleaning out the cacbe:

- `hugo mod clean` cleans things out
