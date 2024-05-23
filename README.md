# Comic_Recommender
A Jupyter Notebook application that uses TF-IDF and Cosine Similarity to recommend comic books by description on customer login or by direct search using dropdown menus or a search bar.

An exercise using an unsupervised NLP model that:
1) Utilizes TF-IDF to create a vector matrix from comic book descriptions or comic book names
2) Utilizes Cosine Similarity to measure vector similarities between descriptions or titles
3) Generates recommendations.

The client, Hideous Mummy Comics, wants to be able to offer comic book recommendations based on a customer's previous purchases. The initial proof of concept of this recommendation system uses the Marvel Comic Books Dataset, found here: https://www.kaggle.com/datasets/deepcontractor/marvel-comic-books. 

The dataset was saved to a PostgreSQL database table, "marvelcomics". A new sequential column called "comic_id" was appended to "marvelcomics", and "customer" and "purchase" tables were added to the database in order to perform dataframe queries involving multiple tables, customer_ids, comic_ids, purchase_ids, purchase_dates, etc. All rows containing null or nan values in the marvelcomics columns "issue_title", "publish_date", "issue_description", "penciler", "writer", and "comic_id" were deleted from the database in pgAdmin 4; deletion of null/nan values in other columns may be required in the future, dependent upon user requirements. 

Database tables were then saved to pandas dataframes, using only the necessary columns for each dataframe. Copies of some dataframes are used to preserve the data in the original dataframes for possible future use.

To test that the recommendation system performs adequately, a mock login page was created. This login page takes a username and password and, upon successful login, displays comic recommendations based on the descriptions associated with the customer's last 3 comic book purchases. There are also buttons displayed to view reports (a bar chart visualizing the customer's preferred titles based on most purchased titles and a list of the titles/number of issues of each title the customer has purchased), a scatterplot illustrating the cosine similarity scores between recommendations based on a title and that title, a wordcloud that visualizes the TF-IDF scores across descriptions, a network graph (a visualization of the cosine similarities of all titles in the marvelcomics dataframe), and an exit button.

The client specifically addressed the issue of offloading comic book backstock. The less popular titles and issues continue to take up physical space in the shop, and the recommendation system needs to allow for comics with less similar descriptions to be recommended. 

However, a way to recommend comics by similar titles (for use by customers, but more specifically for Hideous Mummy's in-store recommendations) is also available to the client, with greater similarity between input titles and recommendations. There are 2 ways to search for a title: using dropdown menus or a search box. 

The dropdown menus produce more accurate recommendations faster, given that the entire selected title is submitted and compared to the titles in the dataframe, as opposed to the search box's input being compared as it is typed, incomplete until the user stops typing. There is also a distinct lag between the finalized recommendations given when using the search box, due to the call to the recommendations_by_search function for each character typed into the search box.

An interactive scatterplot is created when a button is clicked, and displays points for the selected title and its group of recommendations. Hovering over a plotted point will display the comic's title and the cosine similarity score of that title in relation to the title selected.




