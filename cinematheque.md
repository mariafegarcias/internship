
---

<p class="titletext">AUTOMATIZED VIDEO DESCRIPTION</p>

---

<p class="articletext">The "Cinémathèque de Bretagne" has a collection of more than 30000 movies, half of which are amateur and half of which are professional. After their numerization, they are uploaded on the <a href="https://www.cinematheque-bretagne.bzh/" class="linkedinlink">Cinémathèque website</a>, along with a short summary and a few keywords descriptors : </p> 

<figure>
<img src="images/resumecinematheque.png?raw=true" alt="resumecinematheque" class="imgarticle"/>
<figcaption>A typical summary on the website.</figcaption>
</figure>

<figure>
<img src="images/keywordscinematheque.png?raw=true" alt="keywordscinematheque" class="imgarticle"/>
<figcaption>Metadata, including keywords descriptors.</figcaption>
</figure>

<p class="articletext">If you speak French, you will notice that a lot of the words above are highly specific and sometimes impossible to recover from the footage alone, such as the name of the city for instance. During our first meeting with the client, we made it clear that we couldn't expect our algorithm to provide such detailled descriptions, but we could expect to transcribe simple descriptions of the succession of scenes as they are happening on the screen. As for what the final product should look like, we agreed that a simple notebook with detailed instructions was enough, as the clients had already a little bit of experience with running jupyter notebooks.</p>

---

<h1 class="articletext">Scrapping and model choice</h1>
  
<p class="articletext">The first part of our work consisted in retrieving the video direclty from the website, as we didn't have access to the full database. With the client's agreement, we set up a scrapping mechanism that could recover every video from the website, by providing the corresponding id. We then used the library <a href="https://www.scenedetect.com/" class="linkedinlink">pyscenedetect</a> to automatically segment the video into different scenes, by looking for sudden jumps in pixel values on every frame. Once this was done, we began experimenting with various pre-trained models to see which architecture yielded the best results on our dataset. Eventually, it is <a href="https://github.com/salesforce/BLIP" class="linkedinlink">BLIP</a> that took the cake. It performed remarkably well in various context and was overall relatively consistent. The main issue was the vagueness of its description, but given the current state of the art at the time, we did not believe we could make a significant improvement in this area. Fine-tuning the model on keywords and footage from the Cinémathèque was out of the question given our limited time and resources, so we decided to use the model as is. After generating one sentence for every scene, we saved them in a dictionary along with the timestamp associated to the scene. (The clients asked to use the timestamps displayed on the video as reference, instead of the time since the beginning of the video, so we extracted the timestamps using OpenCV) </p>

<figure>
<img src="images/12.png?raw=true" alt="timestamp example" class="imgarticle"/>
<figcaption>An example of a timestamp on a video.</figcaption>
</figure>

---

<h1 class="articletext">Audio transcription</h1>

<p class="articletext">The next step consists in transcribing the audio of the video in order to gain information that could not be accessed otherwise. To do so, we used Google's speech recognition API. Now that we had our description and our audio transcription, we used both to extract the most import keywords that could be used to describe the video. Using NLTK, we can identify the most recurring nouns in all of the text that we recovered so far, and classify those words by number of occurences. After discussing with the client, we decided to only keep words that appeared at least 3 times in total, to minimize the number of false positives. This screened out a few words that were accurate to describe the video, but also mostly words that were hallucinated by either the audio or the visual analysis models, or words that were only marginally present in the film. On average, we managed to extract around 6 words that accurately described the video. We believe that this part of the output could be directly used in production, to provide a minimal amount of metadata to the thousands of videos that are still not referenced on the website. However, for the summary, the model's output is still quite repetitive, mechanical, and not particularly interesting to read. However, we still believe it could be used to help provide a reference for a human transcriptor. Here is the poster we rpoduced to present this project at the end of the year.</p>

<figure>
<img src="images/poster.png?raw=true" alt="poster cinematheque" class="imgarticle"/>
<figcaption>Our presentation poster.</figcaption>
</figure>

<p class="articletext">I would like to thank <a href="https://www.linkedin.com/in/phconze/" class="linkedinlink">Pierre-Henri Conze</a> for tutoring this project, and <a href="https://www.linkedin.com/in/lucie-jullien-89339013/" class="linkedinlink">Lucie Jullien</a> and Nicolas Nogues for collaborating with us.


