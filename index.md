---
layout: default
---

[Contact Me](./contact-jp.html)

STILL WORKING ON THIS! UNDER DEVELOPMENT AS OF 10/10/23

You’ve created your first repository to hold all your work on your new data project on GitHub. Now what? Any typical data science enthusiasts won’t take the time to go through every line of code and file you have, much less an employer from your company of interest. Here’s how they can be led to enjoy your ingenuity.

## 1: Use a README.md file and a GitHub Page

Creating reports on statistics and findings reveals to employers that you know more than just coding and math. The ability to generate digestable reports that are logically follow the process and get to the point is a valued quality of data scientists. In addition, you can choose what to cover in your report: are you most proud of your graphics and visualizations, your experiment's discoveries, or the machine learning algorithms implemented? On GitHub, you have full jurisdiction over what to brag about and the ability to present it on silver platters.

### README.md 

Adding a README.md is simple. On GitHub navigate to your repository. When you see your files you can find a button that says "Add README.MD"

![pic1](/pics/before_readme.png)

When you select it, a new markdown file will open up. When you finish writing, click "commit changes" and write in your commit message. When you finish, your repository should now have a new README.md file and look something like this:

![pic2](/pics/after_readme.png)

GitHub automatically adds the entire README.md file at the bottom of your repo. This is great for employers, because now all information about your project's file system can be summarized in a very convenient spot! 

For more best practices on configuring your README.md file, I recommend using this [link](https://www.freecodecamp.org/news/how-to-write-a-good-readme-file/).

### GitHub Page

Your README.md file can be read as its own website as well. After writing your README.md, find your repository settings and click on "Pages."

![pic3](/pics/blog-step1.png)

Then, click on "Source" and select "GitHub Actions."

![pic4](/pics/blog-step2.png)

You will have two options to choose from: GitHub Pages Jekyll or Static HTML. You can then select one of them, and GitHub will navigate you to a new file with a name depending on which one you select. Then press "commit changes." This will add a hidden file with folder .github/workflows with a new .yml file added. You don't have to do anything with this file. 

Navigate to your repository's settings, revisit "Pages" and a link should now pop on. 

![pic5](/pics/blog-step3.png)

If you click on the link, it will take you to your README.md file as its own website.

![pic6](/pics/blog-step4.png)

Final step! You can add your link to your repository's about section, found on the right of your main file structure. 

![pic7](/pics/blog-step5.png)

Click on the box and GitHub will automatically find your blog's link. You can also add a brief description/abstract and related topics as well (more on that later).  

The information I provided just scratches the surface of setting up a personal website for your repositories. For more information on setting up a blog, I recommend visiting the following sites:

[Creating a GitHub Pages Site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site#creating-your-site)

[Configuring a Publishing Source for GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

[Adding a theme to your GitHub Pages site using Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-a-theme-to-your-github-pages-site-using-jekyll)

[Video: Create an Awesome GitHub Profile Page](https://www.youtube.com/watch?v=9c5xweuO2DA)

[Build A Blog With Jekyll And GitHub Pages](https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/)

## 2: Present Your Data Project as a Linear Process

Data analysis can be especially tricky, as data projects -- especially those involved in research -- are based on purely investigative developments involving lots of trial and error. If you are like me, then you likely have very complex file structures for your projects, and while it makes perfect sense to you, odds are it appears incoherent to viewers. For the entire length of your project, you can easily find yourself diverging into various paths and directions, leading you to dead ends or breakthroughs. 

As important as failure is to personal development, employers mainly care about breakthroughs. In addition, data science employers want to know if you have the skills to follow through on the entire process of a data science project. It's best to align the description of your project as following this process, or in other words, as conveying a set of steps that led you to your ultimate findings and discoveries. 

![pic8](/pics/datasciprocess.jpeg)

In your README.md, GitHub Page, or any other form of presentation, consider following these steps in discussing your data project. 
1. Introduction
  * What is the project about?
  * What were your hypotheses?
2. Data collection
  * Where is your data from?
  * How was it collected?
3. Cleaning
  * How was the data cleaned?
  * How did you handle situations where important data was missing?
  * What did you do to the data to prepare it for analysis?
4. Exploratory Data Analysis (EDA)
  * What trends were discovered?
  * What graphs tell interesting narratives?
5. Model Deployment (and Evaluation)
  * What findings were most significant, and how did they impact the hypotheses?
  * What types of models were implemented into the project?
  * What led you to make your final decisions?

Additional Tips:
* Pictures tell a thousands words -- embed graphs into the blog/README file to augment your report
* Consider adding information about the file structure. For those employers who want to look at your coding scripts, you can link your coding scripts directly to the page/README.md 
* You can showcase code chunks you feel are most impressive/important. This is especially beneficial to show off your ability to code up a modeling technique in a quick view.

```py
# Import the model we are using
from sklearn.ensemble import RandomForestRegressor

# Initiate Random Forest Model
rf = RandomForestRegressor(n_estimators = 1000, random_state = 42)
# Train the model on training data, generate predictions
rf.fit(train_features, train_labels)
predictions = rf.predict(test_features)
```

You can find other views on describing your data project/profile here:

[Building a Data Science Portfolio](https://www.knowledgehut.com/blog/data-science/data-science-portfolio)

[4 Data Science Portfolio Projects You Need to Create](https://builtin.com/data-science/data-science-portfolio-projects)

[Top 10 Data Science Project for 2023](https://365datascience.com/career-advice/top-10-data-science-project-ideas/)


## 3: Pin Your Repository on Your GitHub Profile

You can choose up to six repositories and projects show up when employers access your profile. When you access your main profile page on GitHub, you should see a place on the right of your screen that says "popular repositores" -- the default if you haven't customized your pins. Click "customize your pins" and select which projects you wish to be pinned on your profile. When you are done, your pinned public repositories will be shown on your profile like so...

![pic9](/pics/customizepins.png)

This is important to do, especially when tailoring what kind of projects you desire to showcase. You'll notice that your projects are read by GitHub and detect the names of programming languages -- a nice feature for you to share with employers the hard evidence of your coding skills. 

A more in depth guide:

[Pinning Items to Your Pofile](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-profile/customizing-your-profile/pinning-items-to-your-profile)

## 4: Selecting Topics

Topics are helpful for classifying the contents of your project. Topics mainly have specific usage for enhancing other GitHub search results and finding specialized projects that suit their interests (see [Classifying Your Repository](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/classifying-your-repository-with-topics) for more uses). However, they have special benefits for employers.

Your repository can be classified in such a way that employers can see what kind of work you did, all in a quick summary. For example, did you use a deep learning algorithm to fit your data? Did you tap into a database using SQL? Did your project involve using Python packages in statistics? Did you dive into topics in aviation, finance, psychology, engineering, or any other industry? Whatever you decide to do, simplify it enough for others to know what was involved generally in your data project.   

My Advice on Configuring Topics:
* Keep the number of topics you list minimal. While it widens the depth by which it pops up on a search feed, it complicates the about section of your repo. Know those annoying social media posts with 30 hashtags? Don't be one of those people.
* Best way to maximize the efficiency of the topics section is to have one each listing the programming language(s), project topic/industry, main modelling technique(s), and one read simply as "data-science" or "data-analysis."
* Check out GitHub's [Trending](https://github.com/trending) and [Popular Topics](https://github.com/topics) to see what kind of projects people are most excited about. Your recruiter will be impressed if your work is matching trends within the coding community.  

## 5: Link Your Profile and Repositories to Your LinkedIn Profile and Your Resume/CV

When you've put in all this work on your GitHub before applying for job/internship applications, it is important to make sure that employers know **you have** a GitHub profile. At this point, having just one or two refined repositories can strengthen your profile tremendously. 

### Resume/CV
Your resume is like your "elevator pitch" for a recruiter, meaning that the space on your resume is valuable. Typically, applicants include their GitHub profile on the header of their resume, seen below as an example. 

![pic10](/pics/resumeheader.png)

There are plenty of options to consider:
* Link your repositories/projects under the Projects section of your resume
* List GitHub skills in your application or cover letter
* Mention GitHub as a bullet point in your work experience

Ultimately, your resume has to persuade the recruiter to consider your projects on GitHub as an important part of your introduction. Consider the possibility that you get a job interview. The interviewer will likely reference your resume. If you feasibly reference your GitHub on your resume and prepare your profile/repos for a quick read, then you increase your chances of nailing your interview.  

### LinkedIn
Many job applications are also offered through LinkedIn, and if you choose to apply using your LinkedIn, then implementing your GitHub projects can really improve your application. To add your projects to your LinkedIn profile, navigate to your personal profile.

![pic11](/pics/linkedin-step1.png)

Click on "Add Section", and circulate through the dropdown arrows until you find where it says "Add Projects."

![pic12](/pics/linkedin-step2.png)

You can then add a title and description for your project. After filling in your details, click on "Add Media."

![pic13](/pics/linkedin-step3.png)

It will navigate you to where you can choose to reference a link or a folder. Since your project is on GitHub, you will want to cite a link. 

![pic14](/pics/linkedin-step4.png)

The details ask you for a description of what the link leads to. You can also select a thumbnail. 
GitHub uses an interesting feature. When you use the link to the root file path of your repository, it will automatically fill in the details with the name, description, and a thumbnail showing some GitHub collaborative statistics.  
I recommend citing at least two links per project:
* The source to your repository (github.com/username/name-of-repo/)
* The source to your page/README if applicable (github.io/username/name-of-repo/)

Your finished product would like something like this on your LinkedIn. 

![pic15](/pics/linkedin-step5.png)

## Conclusion



Text can be **bold**, _italic_, or ~~strikethrough~~.

There should be whitespace between paragraphs.

There should be whitespace between paragraphs. We recommend including a README, or a file with information about your project.

# Header 1

This is a normal paragraph following a header. GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

## Header 2

> This is a blockquote following a header.
>
> When something is important enough, you do it even if the odds are not in your favor.

### Header 3

```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
