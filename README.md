wdfn-blog
------------

*The blog for USGS Water Data For The Nation*

# Guidelines for submission
1. Applicable/useful to a greater audience.
2. Content provides additional information not available elsewhere.
3. Relevant to USGS employees or USGS data users
4. Showcases databases, applications, software, or common practices associated with USGS WMA or within the USGS WMA portfolio.

# Submitting an update

1. Fork repo and set up local development environment as needed (see sections below)
2. Create a markdown file in (.md). This should be all lowercase and dashes (e.g. `name-of-post`)
3. Add your markdown file to the `content` folder
4. Include static images in `static\name-of-post`. Images *must* include alt and title text
5. Add a header similar to:

  ```
  ---
  author: Laura DeCicco
  date: 2016-06-16
  slug: plotFlowConc
  draft: True
  type: post
  title: EGRET plotFlowConc using ggplot2
  categories: Data Science
  tags:
    - EGRET
    - R
  image: static/plotFlowConc/unnamed-chunk-4-1.png
  description: Using the R packages, ggplot and EGRET, a new function plotFlowConc        shows a new way to visualize the changes between flow and concentration.
  keywords:
    - EGRET
    - ggplot2
    - data visualization
  author_twitter: DeCiccoDonk
  author_github: ldecicco-usgs
  author_gs: jXd0feEAAAAJ
  author_staff: laura-decicco
  author_email: <ldecicco@usgs.gov>
  author_researchgate: Laura_De_Cicco
    ---
  ```

  Important notes about header:

  * Date format has to be "YYYY-MM-DD" for the updates to be organized properly.

  * Initial submission **must** include `draft: True`

  * `slug` slug will be the name of your url after waterdata.usgs.gov/blog/xxx

  * `image` is not required, but will improve the look of the main "blog" page. Without an image, a generic USGS image will be included.

  * `categories` is a small list of approved options, curated by the managing editor.  They help build the overall site navigation structure.

  * `tags` are more specific words, and do not need to be on a pre-approved list, these will show up on the navigation of the post.

  * `description` will go into a "meta" tag that Google and other sites use

  * `keywords` (can be the same as tags), also go in a "meta" tag to be used by Google and others.

  * It's a good idea to direct people to github issues, emails, or other ways to communicate if they have questions/comments/etc.

  * You can also add single author attributes for the following: twitter handles (`author_twitter`), github (`author_github`), Google Scholor (`author_gs`), ResearchGate (`author_researchgate`), USGS staff profile (`author_staff`), and email (`author_email`)

6. Commit locally and push as needed, then submit a pull request
7. Wait for the pull request to get merged, it will then appear on the dev site.
8. Submitter is responsible for getting 1 internal peer-review of content (interal reviews can be done on a Google Form). Send the reviewer a link to the dev site.
9. A designated approver must sign off on content based on review response
10. A designated web content manager will sign-off on if the page is generally fit to be published on a government website (verify the header follows the "Important notes" above, images contain alt/title tags)
11. Once the content is approved, the draft status can be removed, and the content will appear on the QA site.
12. Assuming all looks good, push to prod

# Tips to writing content
1. If you want to add an image to your content, use the figure shortcode. See < figure > shortcode, https://gohugo.io/content-management/shortcodes/#figure.   There are a few required tags:
   * caption: The caption of the image.  Will be displayed.  Markdown within the caption will be rendered.
   * alt: alt text, for accessibility.  Aim for text that actaully discribes in the image or gif, not just the caption text again.
   * src: path to the image that you want to display.
1. You can use the class ".side-by" if you want your image to only take up 50% of the screen width or if you want to place
two images side by side. You should wrap them in a <div> tag with the class set to "grid-row". Example below:
```html
<div class="grid-row">

{{< figure src="/static/nldi-intro/upstream.png" caption="caption, which can have markdown in it" alt="Description of the image" class="side-by-side" >}}
{{< figure src="/static/nldi-intro/downstream.png" caption="other caption, which can have markdown in it" alt="Description of the image" class="side-by-side" >}}

</div>
```
1. For embedded r code make sure there is a blank line in the markdown between the code and the preceding content text.
1. Use the following markup to implement the ability to Show/Hide code sections:
```html
<button class="toggle-button" onclick="toggle_visibility(this, 'hideMe1')">Show Code</button>
<div id="hideMe1" style="display:none">

``` r
library(jsonlite) 
.
.
.

</div>
```


# Simplified Local development in Windows

Developing without Docker can be simpler on a Windows workstation, particularly if that workstation has software restrictions imposed
by an organization's I.T. department.  There are several ways to make this work and here  is one (relatively) simple example of setting up a development environment.  Stick with us.  This is a bit of time
and learning curve but soon you can be authoring articles and
previewing the results on the your own PC with ease!

**One-time installation steps:**

1. Install and configure Visual Studio Code
   * Visit the Visual Studio Code website and download and install the latest stable version
   * Launch Visual Studio Code. 
   * Install the Git extension.  If wdfn-blog is still hosted on GitHub, it will ask you for login credentials to conveniently integrate this extension with GitHub.  This works really well.

1. Install Git for Windows
   * This step is needed so you can use Git Bash for subsequent steps here.  Skip this step if you I.T. department has already installed this for you.

1. Install Node.js
   * Visit the [node.js](https://nodejs.org/en/) website and download the latest LTS (long-term stable) installer for Windows.
   * Install with default options.  Decline additional complexities such as installing Choclatey or other things the installer offers.

1. Clone the wdfn-blog repo
   * In VS Code, click the source control tab, select "clone repository", then paste in the repo name.
   * If working from wdfn-blog on GitHub, select "clone from GitHub" and you should conveniently see the wdfn-blog fork you have generated.
      * In this tutorial, we have cloned it to D:\sandbox\github-user, under which the cloning process will make the folder wdfn-blog.
   * VS Code will ask you to open this folder.  If you agree, the wdfn-blog project will conveniently always be the one that opens in VS Code when you launch it.  
      * If not, you will need to File->Open Folder, and navigate to the wdfn-blog folder at the location you cloned it.

1. Compile the blog's static assets
   * Launch Git BASH
   * Use the cd command to change to the wdfn-blog directory of the cloned repo.  In this example, it would be `cd /d/sandbox/github-user/wdfn-blog`
   * Use cd to move into the themes directory `cd themes/wdfn_theme/`
   * Install all packages needed to compile assets by typing `npm ci`
      * Note: This is better than running npm install, because npm ci does not change the package-lock.json file, which is a file that rarely needs to be altered.
      * You will see a large node_modules directory appear.  Cool.
   * Compile the blog assets by typine `npm run build`
      * You will see a new directory called static appear.  Great job.

1. Download Hugo and place in path.  
   * Visit [Hugo Releases](https://github.com/gohugoio/hugo/releases) and download the latest proper Windows 64-bit Zipfile.  For example `hugo_0.89.2_Windows-64bit.zip` is the proper file to download as of this writing in November 2021.  Later version should continue to work, as well.
   * Unzip the contents of the Zipfile and move this folder to somewhere convenient and near your cloned repo, such as `D:\sandbox\`
   * Add this folder to your path by right clicking on "This PC" in Windows explorer, selecting properties, searching for "envionment variables" for your account, and adding a new entry.  Paste the Hugo path here.
   * Confirm hugo works in the path by opening Git Bash and typing `hugo env` and confirming it reports the Hugo version.

**Now you are ready for development.  A development cycle should look something like this:**

1. Launch Hugo server
   * Open Git BASH anduse the cd command to change directories to the wdfn-blog (*e.g.,* `cd /d/sandbox/github-user/wdfn-blog`)
   * Launch Hugo server by typing `hugo server --buildDrafts`
      * This will start a local web server.
      * If a firewall issue is raised, contact your I.T. department for an exception.
      * Note the lines that says "web server is available at..." for the next step.
      * Leave this window running, but in the background.  

1. Open the website in a browser
   * Launch your favorite web browser and navigate to the told to you by Hugo.  Usually it's (http://localhost:1313)

1. Launch Visual Studio Code
   * Use File->Open Folder and select the wdfn-blog folder cloned from Git. 
   * It may be open already because the cloning step added it as the active VS Code project.

1. Under the Source Control tab, select "Pull" to get the latest blog updates.

1. Make your edits and additions, view the results in the open web browser
   * Install the FrontMatter extension if you'd like.  It can be a more visually appealing way to manage the metadata for a blog post.
   * When changed are saved, Hugo should detect them, rebuild the page, AND automatically refresh the web browser.

1. Commit and push your changes to Github
   * After you push your changes to Github, you will need to log into Github and create a pull request for these change to go from your fork back to the main master.  This is the step where you can request a peer review of your work.


Note: There are numerous other options for installing both Node and Hugo, through a package manager such as `apt-get` for Linux, [Homebrew](https://brew.sh/) for MacOS, or [Chocolatley](https://chocolatey.org/) for Windows.  This tutorial bypasses a package manager because some I.T. departments may not approve of that
form of software.


# Local development with Docker

A Dockerfile and Docker Compose configuration is provided that is capable of running a development server and building the deployable static site.

Using `docker-compose`, you may run a development server on http://localhost:1313:

```bash
docker-compose up
```

The default server instance will include draft articles.

If the site on http://localhost:1313 is missing various static files, you may need to first run the following command to rebuild assets:

```bash
docker-compose run hugo build --buildDrafts
```
If you haven't set things up on the right cert bundle, it may be easier to run this command outside the USGS VPN.

Once that is done, you can use `docker-compose up` to start the development server again.

## Debugging the container

If the need arises, you may run arbitrary commands in the container, such as a bash shell:

```bash
docker-compose run hugo bash -l
```

# Build static site using Docker

Using `docker-compose`, the site may be built using the `build` command provided by the container:

```bash
docker-compose run hugo build
```

The base URL is specified with the `HUGO_BASEURL` environment variable:

```bash
docker-compose run -e HUGO_BASEURL=http://dev-owi.usgs.gov/blog/ hugo build
```

Additional arguments may be passed to the [**Hugo**](https://gohugo.io/) binary as the last argument:

```bash
docker-compose run hugo build --buildDrafts
```


# Instructions for R users

[**Templates for R markdowns**](https://github.com/USGS-R/USGSmarkdowntemplates)

```r
remotes::install_github('usgs-r/USGSmarkdowntemplates')
```

This will add `draft: True` to the markdown header (not rmarkdown file). It is up to you to remove that AFTER the content has been reviewed.

Make sure to format your blog a .md file, not a .Rmd file (which is the deafult if using a package such as blogdown).There are some simple functions for converting between the two if using R. 

When setting up a new project in RStudio, there are many ways to connect to the project. One is by starting a new project, then choose version control, select Git and use the URL "https://github.com/username/wdfn-blog.git". This should allow you to use Git push, pull, and merge code within RStudio.


Disclaimer
----------
This software is preliminary or provisional and is subject to revision. It is being provided to meet the need for timely best science. The software has not received final approval by the U.S. Geological Survey (USGS). No warranty, expressed or implied, is made by the USGS or the U.S. Government as to the functionality of the software and related material nor shall the fact of release constitute any such warranty. The software is provided on the condition that neither the USGS nor the U.S. Government shall be held liable for any damages resulting from the authorized or unauthorized use of the software.
