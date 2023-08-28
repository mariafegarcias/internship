
---

<p class="titletext">EVOLUTION OF MUSICAL TRENDS OVER THE YEARS WORLDWIDE</p>

---

<p class="articletext"> This project was realised in collaboration with three other students of IMT Atlantique : <a href="https://www.linkedin.com/in/martin-rouesn%C3%A9-81a489182/" class="linkedinlink">Martin Rouesné</a>, <a href="https://www.linkedin.com/in/camillefrancoismartin/" class="linkedinlink">Camille François-Martin</a> and <a href="https://www.linkedin.com/in/guyllian-gomez/" class="linkedinlink">Guyllian Gomez</a>.</p>

---

<h1 class="articletext">Dataset and objectives</h1>

<p class="articletext"> We scrapped the top 100 weekly Youtube charts since 2016 from over 60 countries and analyzed their main musical characteristics using Spotify's API. The API provides informations on various aspects such as the song's length, key, tempo and loudness, as well as pre-made metrics such as "danceability", "acousticnes" or "valence", which describes the felt sadness/hapiness of the song. The following diagram details the way our data was acquired and structured.</p>

<figure>
<img src="images/flow1spotify.png?raw=true" alt="flow1" class="imgarticle"/>
<figcaption>Acquisition of the dataset.</figcaption>
</figure>

<p class="articletext">Our objective was ultimately to create a model capable of predicting the popularity of any given song in various countries, and at different time periods. This model could serve as tool for market analysis, to guide the promotional campaign of upcoming artists. Before building the model, I was tasked with developping visualizations to help our team better grasp the dataset, and find interesting trends and correlations. </p>

---

<h1 class="articletext">Temporal analysis</h1>

<p class="articletext">We can perform a first basic analysis by checking the evolution of some characteristics over the years. For instance, the average song duration has increased over the year in some countries, like South Africa, but diminished in other, like in Japan, and has overall stayed the same worldwide.</p>

<figure>
<img src="images/duration.png?raw=true" alt="duration" class="imgarticle"/>
<figcaption>Evolution of the average song lenght over time in Japan, South Africa, and worldwide.</figcaption>
</figure>

<p class="articletext">Other characteristics seem to follow a periodic trend. That's the case of "danceability" in Italy and France, which always jumps in summer. </p>

<figure>
<img src="images/danceability.png?raw=true" alt="danceability" class="imgarticle"/>
<figcaption>Evolution of danceability over time in France, Italy, and worldwide. Summer period is colored in yellow.</figcaption>
</figure>

---

<h1 class="articletext">Plotting correlations</h1>

<p class="articletext">For a more thorough inspection, we can calculate the correlation between each characteristic and the average performance of songs possessing this characteristic in a country. We can also split the results by week for maximum specificity. This gives us some nice insight that I chose to display in a circular fashion to account for the periodic nature of musical trends that we highlighted above. This powerful way of vizualising gives us immediately the broad trend over the year for a specific country. For instance, in Italy, There seem to be a massive popularity "of high-valence" (aka happy) songs between the weeks 25 to 24, which corresponds roughly to summer. </p>

<figure>
<img src="images/wheel_Italy.png?raw=true" alt="wheel_Italy" class="imgarticle"/>
<figcaption>Who would have thought that Italians enjoy happy songs in the summer?</figcaption>
</figure>

<p class="articletext">Though this could be easily expected, there are still huge differences in the correlations across various countries. For instance, the Nicaraguan wheel looks rather different from the Italian one : </p>

<figure>
<img src="images/wheel_Nicaragua.png?raw=true" alt="wheel_Nicaragua" class="imgarticle"/>
<figcaption>Nicaraguans like to dance all year long.</figcaption>
</figure>

<p class="articletext">Just for fun, let's plot every country at the same time and animate based on the current week of the year</p>

<figure>
<img src="images/featuresovertheyear.gif?raw=true" alt="features over the year" class="imgarticle"/>
<figcaption>It's not very informative, but I think it's cool.</figcaption>
</figure>

<p class="articletext">Even though this last animation highlights both a great diversity across countries and some variability over time, we need to keep in mind that the correlations showed here are rather weak on average, as most of them are below 0,2. This is a hint that it would be hard to produce a predictive model based solely on these explanatory variables.</p>

---

<h1 class="articletext">PCA exploration</h1>

<p class="articletext">We can make another interesting visualization by performing PCA on the 10 explanatory variables, and plot each countries in the resulting latent space. This allows us to see immediately which countries are "close" to each other and which one are "far away" in their musical tastes. From this first plot, it appears that Dominican Republic, Indonesia and Japan like very different songs.</p>

<figure>
<img src="images/PCAcountry.png?raw=true" alt="PCA country" class="imgarticle"/>
<figcaption>Every country is a different point in the PCA space.</figcaption>
</figure>

<p class="articletext">Let's color the points by continent :</p>

<figure>
<img src="images/PCAcontinents.png?raw=true" alt="PCA country" class="imgarticle"/>
<figcaption>Every point is a country, colored by continent.</figcaption>
</figure>

<p class="articletext">Interestingly, it seems like Europe has overall similar tastes, South America has very similar tastes, which could maybe be explained by the massive popularity of Reggaeton in the whole continent. The pale blue dot separated from the rest of the African countries is South Africa, but it is Asia that seems to have the most diverse musical culture overall. </p>

---

<h1 class="articletext">Conclusion</h1>

<p class="articletext">That's the bulk of the data vizualisation I performed for this project. Of course, with such an interesting and rich database, there is a lot more that could be said, but for the purpose of this project, the aim of this work was to explore possibilities to guide our effort in the making of a predictive algorithm using only the musical characteristics provided by Spotify. As we have seen from the weak correlations obtained, even after segmenting the data by country and time, it was to be expected that even our best classification model, which turned out to be an XGBoost algorithm, would struggle to yield satisfying results. I believe therefore that this study is a perfect illustration of the importance of these kinds of preparatory steps before investing time and money building a model. In this case, it would have been good to try to include more variables to see if it could add more explanatory power.</p>
