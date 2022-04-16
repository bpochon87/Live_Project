# Live_Project

<h3>Index</h3>
<ul>
  <li><a href="#intro">Description of Project</a></li>
  <li><a href="#bs">Scraping Data via BeautifulSoup</a></li>
  <li><a href="#api">Sourcing Data via an API</a></li>
</ul>



<h3 id="intro">Description of Project</h3>
<p>As part of our curriculum, we were tasked with a two-week sprint where we had to implement our own application (website) nested within the main application. This was done with other students as my teammates and instructors as project managers. Working according to the Agile methodology and within the scrum framework, I completed multiple stories where I created a smooth and navigable UI while defining a UX.</p>

<p><strong>My website allowed for:</strong></p>
<ul>
  <li>creation of a mountain-bike (MTB) trail review.</li>
  <li>updating or deleting that MTB trail review.</li>
  <li>viewing data from a top-ten MTB list scraped from another website.</li>
  <li>viewing data from an API that provided MTB trails in central Colorado.</li>
</ul>

<p><strong>Technologies used by me were:</strong></p>
<ul>
  <li>Django</li>
  <li>Azure DevOps</li>
  <li>Python</li>
  <li>HTML</li>
  <li>CSS</li>
</ul>

<h3 id="bs">Scraping Data via BeautifulSoup</h3>
<p>I implemented a page scrape of data that I wanted using the BeautifulSoup package in Python.</p>

```
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
  


  
