# new-salem-pelican
New Salem running on Pelican

## Initial Set Up

- Clone the repo.
- In the project directory, initialize the theme submodule: `git submodule init && git submodule update`
- Run `pipenv update` to grab dependencies.

## Running the Project.
- Open pipenv shell: `pipenv shell`
- Run the web server: `make devserver`

## Static files and make targets
The typical Pelican structure is complicated by the large number of legacy static files from the Old Salem site that have not been converted into Pelican markdown content as well as static HTML files that replace or link to these unmanaged static files. In order to limit the pollution of the content directory, these files reside inside a number of discrete subdirectories:

`old-salem` - Old Salem static web content, some changed minimally to conform to New Salem urls and content requirements
`static-salem` - New Salem static web content unmanaged by Pelican
`static-salvrec` and `static-uph1wit` - New Salem static content that was built once by Pelican from markdown files in the `content` directory, but made into static web content because we don't expect them to be modified going foward.

The order that these files should be loaded into the output directory is:
1. `old-salem`
2. Pelican-built content
3. `static-salem`, `static-salvrec`, `static-uph1wit` (implying that none of these files should conflict)

These map over to the following Make targets:

* `make html` performs steps 1, 2, and 3. 
* `make html-static` performs only step 3, in case the pelican build overwrites something in static-salem.
* `make devserver` extends `make html-old`
* `make publish` and its child targets clean the output directory and then perform steps 1, 2, and 3.

## Documentation
[Documentation for the Salem Witchcraft Papers](docs/SWPdocs.md)
