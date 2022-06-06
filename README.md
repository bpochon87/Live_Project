# Live_Project

<h2 align="center">Mountain Bike Trail Review Website</h2>

![homepage.png](images/homepage.png)

<h2>Index</h2>
<ul>
  <li><a href="#intro">Description</a></li>
  <li><a href="#bs">Scraping Data</a></li>
  <li><a href="#api">Sourcing Data</a></li>
  <li><a href="#ux">Video: The UI and UX</a></li>
  <li><a href="#skills">In Finality: Skills</li>
</ul>



<h2 id="intro">Description</h2>
<p>As part of our curriculum, we were tasked with a two-week sprint where we had to implement our own application (website) nested within the main application. This was done with other students as my teammates and instructors as project managers. Working according to the Agile methodology and within the scrum framework, I completed multiple stories where I created a smooth and navigable UI while defining a UX.</p>

<p><strong>My website allowed for:</strong></p>
<ul>
  <li>creation of a mountain-bike (MTB) trail review,</li>
  <li>updating or deleting that MTB trail review,</li>
  <li>viewing data from a top-ten MTB list scraped from another website, and</li>
  <li>viewing data from an API that provided MTB trails in central Colorado.</li>
</ul>

<p><strong>Technologies used by me were:</strong></p>
<ul>
  <li>Django</li>
  <li>Azure DevOps</li>
  <li>Python</li>
  <li>HTML</li>
  <li>CSS</li>
  <li>REST API</li>
</ul>

<h2 id="bs">Scraping Data via BeautifulSoup</h2>
<p>One story required the use of the Python package BeautifulSoup to scrape data from an existing webpage. Check out the code and screenshot.</p>

```python
## Beautiful Soup webpage scraping.
## View for scraping our selected page.
def top_mtb(request):
    # Empty list for use in for loop.
    top_bikes = []
    
    # Empty list for use in for loop.
    bike_desc = []
    
    # Empty list for use in last for loop. This loop concatenates the other two lists.
    full_bike_desc = []
    
    # URL to be scraped.
    page = requests.get('https://www.outdoorgearlab.com/topics/biking/best-mountain-bike')
    
    # Setting soup object using the particular html parser.
    soup = BeautifulSoup(page.content, 'html.parser')
    
    # Accessing second 'articletext' class as there are two used (and we want the second only).
    parent = soup.find_all('div', class_='articletext')[1:]
    
    # This for loop iterates through the 'h2' tags within the class 'articletext'.
    # They are put into the blank 'bike_desc' list.
    for i in parent:
        desc = i.find_all('h2')
        for j in desc:
            desc_txt = j.text
            bike_desc.append(desc_txt)

    # This second body of the for loop iterates through the 'h3' tags within 'articletext'.
    # They are put into the blank 'top_bikes' list.
        bike = i.find_all('h3')
        for x in bike:
            bike_txt = x.text
            top_bikes.append(bike_txt)
            
    # New list containing only the elements we want from both lists.
    new_desc_list = bike_desc[0:8]
    new_top_bike_list = top_bikes[0:8]

    # Joining together list elements since we have two separate lists above.
    z = 0
    for desc in new_desc_list:
        bike_model = new_desc_list[0 + z] + ': ' + new_top_bike_list[0 + z]
        full_bike_desc.append(bike_model)
        z += 1

    context = {'full_bike_desc': full_bike_desc}
    return render(request, 'MTB_Trails/top_mtb.html', context)
```

![scrapedData.png](images/scrapedData.png)


<h2 id="api">Sourcing Data via an API</h2>
<p>Another story had me locating an API that would be suitable for my particular use and implementing it as a source of data. I brought in all data provided and then selected only certain parameters (name of trail, description, difficulty [if specified]) that I wanted to pass to my webpage. Check out the code and video.</p>

```python
def trail_api(request):
    # API code from https://rapidapi.com/trailapi/api/trailapi/
    url = "https://trailapi-trailapi.p.rapidapi.com/trails/explore/"

    # Latitude and longitude required. 'per_page' and 'radius' optional.
    parameters = {"lat": "39", "lon": "-106", "per_page": "300", "radius": "100"}
    headers = {
        "X-RapidAPI-Host": "trailapi-trailapi.p.rapidapi.com",
        "X-RapidAPI-Key": "e3b28ce81fmshbcd98af11e9812dp1487c5jsnaf6f45c8d994"
    }
    response = requests.request("GET", url, headers=headers, params=parameters)
    json_response = response.json()

    # Empty lists to populate with data we want to pull from the API.
    trail_name_list = []
    trail_desc_list = []
    trail_city_list = []
    trail_difficulty_list = []

    # Populating all lists except 'trail_list'.
    for item in json_response['data']:
        trail_name_list.append(item['name'])
        trail_desc_list.append(item['description'])
        trail_city_list.append(item['city'])
        trail_difficulty_list.append(item['difficulty'])

    trail_list = zip(trail_name_list, trail_desc_list, trail_city_list, trail_difficulty_list)

    context = {'trail_list': trail_list}
    return render(request, 'MTB_Trails/trail_api.html', context)
```

https://user-images.githubusercontent.com/83652607/163685974-1b9bfa39-7bef-42be-8d77-abe1d7a1a5c4.mp4


<h2 id="ux">Video Showcasing UI and UX</h2>
<p>I was quite pleased to see how the website came together: the melded colors, the slick and straightforward interface. Please enjoy a quick video of the functionality and pages created within the Django framework.</p>

https://user-images.githubusercontent.com/83652607/163687482-6487c094-b23f-4123-ab4c-523008ec2681.mp4

<h2 id="skills">In Finality: Skills</h2>
<p>This project allowed me to further hone several skills. They include:</p>
<ul>
  <li>Coding <strong>Python</strong></li>
  <li>Coding <strong>CSS</strong></li>
  <li>Coding <strong>HTML</strong></li>
  <li>Working within the <strong>Django</strong> framework</li>
  <li>Working with an <strong>MVC</strong> architectural pattern</li>
  <li>Working with <strong>APIs</strong></li>
  <li>Working within the <strong>Scrum</strong> framework</li>
  <li>Working with the <strong>Agile</strong> methodology</li>
</ul>

<p>Overall, <strong>communication</strong> with project managers and co-workers was one of the master keys which led to a successful venture.</p>
<br>
<p>Thank you for your time.</p>




  
