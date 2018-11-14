# Leroy Merlin Russia Technology Radar <!-- omit in toc -->

- [What is the Technology Radar?](#what-is-the-technology-radar)
- [What is the purpose?](#what-is-the-purpose)
- [How do we maintain it?](#how-do-we-maintain-it)
- [Radar in Action](#radar-in-action)
- [How To Use](#how-to-use)
     - [Setting up your data](#setting-up-your-data)
     - [Sharing the sheet](#sharing-the-sheet)
     - [Using CSV data](#using-csv-data)
     - [Building the radar](#building-the-radar)
     - [More complex usage](#more-complex-usage)
- [Docker Image](#docker-image)
- [Contribute](#contribute)
     - [Don't want to install node? Run with one line docker](#dont-want-to-install-node-run-with-one-line-docker)

## What is the Technology Radar?

The Leroy Merlin Russia Technology Radar is a list of technologies, complemented by an assessment result,
called *ring assignment*. We use four rings with the following semantics:

- **ADOPT** - Technologies we have high confidence in to serve our purpose, also in large scale.
     Technologies with a usage culture in our Leroy Merlin Russia production environment, low risk and
     recommended to be
     widely used.

- **TRIAL** - Technologies that we have seen work with success in project work to solve a real
     problem; first serious usage experience that confirm benefits and can uncover limitations. TRIAL
     technologies are slightly more risky; some engineers in our organization walked this path and will share
     knowledge and experiences.

- **ASSESS** - Technologies that are promising and have clear potential value-add for us;
     technologies worth to invest some research and prototyping efforts in to see if it has impact. ASSESS
     technologies have higher risks; they are often brand new and highly unproven in our organisation. You will
     find some engineers that have knowledge in the technology and promote it, you may even find teams that have
     started a prototyping effort.

- **HOLD** - Technologies not recommended to be used for new projects. Technologies that we think
     are not (yet) worth to (further) invest in. HOLD technologies should not be used for new projects, but
     usually can be continued for existing projects.

## What is the purpose?

The Technology Radar is a tool to inspire and support engineering teams at Leroy Merlin Russia to pick the
best technologies for new projects; it provides a platform to share knowledge and experience in technologies,
to reflect on technology decisions and continuously evolve our technology landscape. Based on the [pioneering work of ThoughtWorks](https://www.thoughtworks.com/radar), our Technology Radar sets out the changes in technologies that are interesting in
software development - changes that we think our engineering teams should pay attention to and consider
using in their projects.

## How do we maintain it?

The Technology Radar is maintained by the *Leroy Merlin Russia Technology Community* - an open
group of senior Leroy Merlin Russia technologists committed to devote time to the Technology Radar purpose.
The community is sponsorted by CTO and self organises to maintain the Technology Radar documents,
including this public version. Assignment of technologies to rings is the
outcome of ring change proposals, which are discussed and voted on in Technology Strategy Board meetings.
The Tech Radar depends on active participation and input from all engineering teams at Leroy Merlin Russia.

## Radar in Action

You can see this in action at [Leroy Merlin Russia Technology Radar](https://adeo.github.io/lmru-technology-radar).

## How To Use

A library that generates an interactive radar, inspired by [thoughtworks.com/radar](http://thoughtworks.com/radar).

The easiest way to use the app out of the box is to provide a *public* Google Sheet ID from which all the data will be fetched. You can enter that ID into the input field on the first page of the application, and your radar will be generated. The data must conform to the format below for the radar to be generated correctly.

### Setting up your data

You need to make your data public in a form we can digest.

Create a Google Sheet. Give it at least the below column headers, and put in the content that you want:

| name          | ring   | quadrant               | isNew | description                                             |
| ------------- | ------ | ---------------------- | ----- | ------------------------------------------------------- |
| Composer      | adopt  | tools                  | TRUE  | Although the idea of dependency management ...          |
| Canary builds | trial  | techniques             | FALSE | Many projects have external code dependencies ...       |
| Apache Kylin  | assess | platforms              | TRUE  | Apache Kylin is an open source analytics solution ...   |
| JSF           | hold   | languages & frameworks | FALSE | We continue to see teams run into trouble using JSF ... |

### Sharing the sheet

* In Google sheets, go to 'File', choose 'Publish to the web...' and then click 'Publish'.
* Close the 'Publish to the web' dialog.
* Copy the URL of your editable sheet from the browser (Don't worry, this does not share the editable version). 

The URL will be similar to [https://docs.google.com/spreadsheets/d/1waDG0_W3-yNiAaUfxcZhTKvl7AUCgXwQw8mdPjCz86U/edit](https://docs.google.com/spreadsheets/d/1waDG0_W3-yNiAaUfxcZhTKvl7AUCgXwQw8mdPjCz86U/edit). In theory we are only interested in the part between '/d/' and '/edit' but you can use the whole URL if you want.

### Using CSV data
The other way to provide your data is using CSV document format.
You can enter any URL that responds CSV data into the input field on the first page.
The format is just the same as that of the Google Sheet, the example is as follows:

```
name,ring,quadrant,isNew,description  
Composer,adopt,tools,TRUE,"Although the idea of dependency management ..."  
Canary builds,trial,techniques,FALSE,"Many projects have external code dependencies ..."  
Apache Kylin,assess,platforms,TRUE,"Apache Kylin is an open source analytics solution ..."  
JSF,hold,languages & frameworks,FALSE,"We continue to see teams run into trouble using JSF ..."  
```

Note: The CSV file parsing is using D3 library, so consult the D3 documentation for the data format details.

### Building the radar

Paste the URL in the input field on the home page.

That's it!

Note: the quadrants of the radar, and the order of the rings inside the radar will be drawn in the order they appear in your data.

### More complex usage

To create the data representation, you can use the Google Sheet [factory](/src/util/factory.js) or CSV, or you can also insert all your data straight into the code.

The app uses [Tabletop.js](https://github.com/jsoma/tabletop) to fetch the data from a Google Sheet or [D3.js](https://d3js.org/) if supplied as CSV, so refer to their documentation for more advanced interaction.  The input data is sanitized by whitelisting HTML tags with [sanitize-html](https://github.com/punkave/sanitize-html).

The application uses [webpack](https://webpack.github.io/) to package dependencies and minify all .js and .scss files.

## Docker Image
We have released BYOR as a docker image for our users. The image is available in our [DockerHub Repo](https://hub.docker.com/r/wwwthoughtworks/build-your-own-radar/). To pull and run the image, run the following commands.

```
$ docker pull wwwthoughtworks/build-your-own-radar
$ docker run --rm -p 8080:80 -e SERVER_NAMES="localhost 127.0.0.1" wwwthoughtworks/build-your-own-radar
$ open http://localhost:8080
```

## Contribute

All tasks are defined in `package.json`.

Pull requests are welcome; please write tests whenever possible. 
Make sure you have nodejs installed.

- `git clone git@github.com:thoughtworks/build-your-own-radar.git`
- `npm install`
- `npm test` - to run your tests
- `npm run dev` - to run application in localhost:8080. This will watch the .js and .css files and rebuild on file changes

### Don't want to install node? Run with one line docker

     $ docker run -p 8080:8080 -v $PWD:/app -w /app -it node:7.3.0 /bin/sh -c 'npm install && npm run dev'

After building it will start on localhost:8080
