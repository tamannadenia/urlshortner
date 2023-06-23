# URL-Shortener

URL Shortener with multiple features 

## Features:

🎈1. Added a hits count (for each Short URL) tracker to keep track of how frequently people visit any website using a short link created by the project website.


🎈Use the ShortURL you created to keep track of the number of times a site has been accessed.

🎈 Maintained a table on the home page listing all the URLs created thus far.

🎈 You can search the associated data of your ShortURL(in case you don't want to look for it in the table) by using the search box.


## Tech Stacks

🦕 **Client:** HTML, CSS, Bootstrap, JS, EJS

🦕 **Server:** Node, Express

🦕 **Database:** MongoDB

## Run Locally

Go to project directory

```bash
  cd URL Shortner
```

Clone the project

```bash
  git clone https://github.com/Ukriyte/URL-Shortner.git
```

Initialize package.json

```bash
  npm init -y
```

Install dependencies

```bash
  npm i mongoose express shortid ejs
```

Install node and mongodb compass on your device locally and add the path of there respective bin files to your device environment variables.
Note: Your mongodb application should be running in the background.

Edit the following code present in the beginning of server.js file and put the mongodb host url shown in mongodb compass

```bash
  //Mongo db connection
mongoose.connect('mongodb://127.0.0.1:27017', {
    useNewUrlParser: true, useUnifiedTopology: true
})

```
Start the server

```bash
  node .\server.js
```

Search the following in the browser and URL shortner will open up

```bash
  http://localhost:5000
```

## Internal Wokring:

### Short URLs that lead back to the original URL 

Whenever anyone searchs for a shortURL, the backend processes the get request. It searchs if the ShortUrl id is present in the database,
 if not then an error is returned. If it is present then the browser is redirected to the long URL. Also the number clicks is incremented and saved to database. This is done by the following piece of code:
 
 ```bash
 app.get('/:shortUrl', async (req,res) =>{
    const shortUrl = await ShortUrl.findOne({ short: req.params.shortUrl})
    if(shortUrl == null) return res.sendStatus(404)
    shortUrl.Clicks++
    shortUrl.save()
    res.redirect(shortUrl.full)
})
```
     
### Search Mechanism:

A search can be done on the basis of ShortUrl id, long URL and notes. Whenever the required field is put in the search box and search button is clicked,
the backend recieves a post request and checks for the input in all three parameters. If it does not find any matching object, it returns a NOT found error
If it is found then a new page is rendered(search.ejs) and all the information of the url is shown. Check the following code snippet for refernce:

```bash
//Sending search request to backend from searchInput field and finding matching
//value in database and rendering new site with link that was searched for
app.post('/search', async (req,res) =>{
    const temp1 = await shortUrl.findOne({Notes : req.body.searchInput}) 
    if(temp1==null){
        const temp2 = await shortUrl.findOne({short : req.body.searchInput}) 
        if(temp2==null){
            const temp3 = await shortUrl.findOne({full : req.body.searchInput})
            if(temp3==null){
                return res.sendStatus(404)
            }
            else{
                res.render('search', {longsearch1: temp3.full, longsearch2: temp3.short,
                    longsearch3: temp3.Clicks, longsearch4: temp3.Notes });
                } 
        }
        else{
            res.render('search', {longsearch1: temp2.full, longsearch2: temp2.short,
                longsearch3: temp2.Clicks, longsearch4: temp2.Notes });
            }
    }
    else{
        res.render('search', {longsearch1: temp1.full, longsearch2: temp1.short,
            longsearch3: temp1.Clicks, longsearch4: temp1.Notes });
        }
    
})
//1 route for three different parameters
```
## Resources used:

### Youtube Tutorials:

https://www.youtube.com/watch?v=oSIv-E60NiU&ab_channel=CodeWithHarry

https://www.youtube.com/watch?v=SccSCuHhOw0&ab_channel=WebDevSimplified

https://www.youtube.com/watch?v=XlvsJLer_No&list=PLZlA0Gpn_vH8jbFkBjOuFjhxANC63OmXM&ab_channel=WebDevSimplified

https://www.youtube.com/watch?v=IqpfBGsALqc&list=PL7sCSgsRZ-slYARh3YJIqPGZqtGVqZRGt&ab_channel=WalkThroughCode

### Documetations:

https://mongoosejs.com/docs/index.html

https://getbootstrap.com/docs/5.3/getting-started/introduction/

## Key Takeaways:

💫 The URL shortener project allowed for the practical application of full-stack development, integrating frontend (HTML, CSS, Bootstrap, EJS) and backend (Node.js, Express, MongoDB) technologies.

💫 Learning outcomes included integrating MongoDB for database functionality, and exploring URL shortening techniques, search functionality, and user interface design.

💫 The project emphasized error handling, documentation, project organization, and provided opportunities for continuous improvement and future enhancements.

## THANK YOU .

