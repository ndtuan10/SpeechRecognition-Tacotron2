# SpeechRecognition-Tacotron2

 ![uitlogo](https://portal.uit.edu.vn/Styles/profi/images/logo186x150.png)

- Contents of projects of Speech Recognition / Speech Synthesis (Tổng hợp giọng nói - CS535): pre-trained two models -  Tacotron2 and WaveGlow.

## **Introduction to data**
- In this experimental, we use an English dataset named “LJ Speech Dataset” with the latest version version 1.1. This is a speech data set consisting of 13,100 short audio clips of a person reading from excerpts from 7 non-fiction books. Each recording is provided for each audio track. These audio clips vary in length from 1 second to 10 seconds and have a total duration of about 24 hours.
- For more information about dataset, please read more here. https://github.com/ndtuan10/SpeechRecognition-Tacotron2/blob/main/data/LJSpeech-1.1.md
- Link dataset: https://keithito.com/LJ-Speech-Dataset/

## **Training the model**
- We use 2 pre-trained models
  - Tacotron2 pre-trained models https://github.com/NVIDIA/tacotron2
    - Để download checkpoint: https://drive.google.com/file/d/1c5ZTuT7J08wLUoVZ2KkUs_VdZuJ86ZqA/view
![image](https://github.com/ndtuan10/SpeechRecognition-Tacotron2/blob/main/Tacotron-2-system-arch.png)
  - WaveGlow pre-trained models - https://github.com/NVIDIA/waveglow
    - Để download checkpoint: https://drive.google.com/file/d/1WsibBTsuRg_SF2Z6L6NFRTT-NjEy1oTx/view
![image](https://github.com/ndtuan10/SpeechRecognition-Tacotron2/blob/main/WaveGlow-network.png)
- For details on how to train 2 pre-trained models and how to synthesize speech, please read the following notebook. 
https://github.com/ndtuan10/SpeechRecognition-Tacotron2/blob/main/Speech-recognition%20using%20pre-trained%20(Tacotron2%2BWaveGlow).ipynb

## **Evaluation the model**
- To evaluate the quality of our speech synthesis model using Tacotron2 and WaveGlow, we selected 25 texts for testing. We use the average of MOS score of 2 listeners to derive a quality level based on the human ear.
- For details about model evaluation by MOS, please read here https://github.com/ndtuan10/SpeechRecognition-Tacotron2/blob/main/Model%20evaluation%20by%20MOS.pdf
- Table for determining the rating scale MOS

Score |1 |2 |3 |4 |5
--- | --- | --- | --- | --- | ---
Label | Very bad | Bad | Medium | Good | Excellent

## **Introduction to testing data**
- We recommend any 25 texts, with all genres, from the content is poetry, sports news, weather forecast, song lyrics, speeches, famous sayings, exclamations, question,….
- For details about introduction to testing data, please read here.
https://github.com/ndtuan10/SpeechRecognition-Tacotron2/blob/main/Introduction%20to%20testing%20data.pdf
- Table for some examples are text for experiment

STT |Content 
--- | ---
1 | My love for you is like the raging sea. So powerful and deep it will forever be. Through storm, wind, and heavy rain. It will withstand every pain.
2 | Amazing good job, you!
3 | Manchester City kept their hopes of winning a fourth consecutive Carabao Cup alive after overcoming Manchester United 2-0 in their semi-final at Old Trafford.
4 | Roger Federer led 4-1, and 30-0 in the second set.
5 | Hanoi capital continue to get cold air which flows from the North, the temperature may drop under 15 degrees, so citizens should keep the bodies warm.
... | ...
... | ...
23 | And the memories bring back, memories bring back you.
24 | I woke up early this morning. So I went to school on time.
25 | And all my love, I’m holding on forever. Reaching for the love that seems so far.

## **Text synthesis**
- We enter a text in English in any “TEXT” section, for example: *“My love for you is like the raging sea. So powerful and deep it will forever be. Through storm, wind, and heavy rain, it will withstand every pain”*. In terms of meaning, we roughly translate *"Tình yêu anh dành cho em giống như biển cả đang điên cuồng. Quá mạnh mẽ và sâu sắc, nó sẽ luôn mãi mãi như vậy. Băng qua bão, gió và mưa lớn. Nó sẽ chịu đựng được tất cả mọi nỗi đau"*.
- So this is a text like a verse. As a result, we expect the Tacotron2 and WaveGlow models to deliver a soothing, soulful reading.
- Then we convert that text into a mel spectrogram, and plot it using the matplotlib library.
![image](https://github.com/ndtuan10/SpeechRecognition-Tacotron2/blob/main/mel-spectrogram-result.png)

- Output audio by converting the generated mel spectrogram to audio. We use WaveGlow in inference and run using the output of the mel spectrogram when passing through the post-net, with sigma = 0.666 used to denoise the mel spectrogram and sampling rate = 22.050 kHz per second.
- As a result, we get a 11-second audio female voice reading from the entered English text above. We can download this audio and listen from here. https://github.com/ndtuan10/SpeechRecognition-Tacotron2/blob/main/result.wav
## **Introduction to evaluation criteria and experimental results table**
- For details about introduction to evaluation criteria and experimental results table, please read here.
https://github.com/ndtuan10/SpeechRecognition-Tacotron2/blob/main/Introduction%20to%20evaluation%20criteria%20and%20experimental%20results%20table.pdf
- Experimental results table

System |MOS 
--- | ---
Tacotron2 + WaveGlow (1st person) | 3.82
Tacotron2 + WaveGlow (2nd person) | 3.65
**Tacotron2 + WaveGlow (medium)** | **3.735**

## **In conclusion**
- According to our assessment, after training two pretrained Tacotron2 and WaveGlow models, we find our model can handle different types of text from weather forecasting, reading stories, reading news ... with a voice that sounds natural and fluent like a human voice. Especially, with exclamations and questions, the voice of the reader tends to increase the intonation at the end of the sentence, and with the words "you're", the voice still gives the correct reading of this word.
- The Tacotron 2 and WaveGlow models form a TTS (text-to-speech) system that allows users to synthesize natural sounding voices from raw recordings without any additional information, capable of producing high quality voices from mel spectrograms, combining details from Glow and WaveNet enables fast, efficient speech synthesis with a simple model that is easy to train.
- Despite having a high-quality and clear voice, it still does not response our requirements when reading poetry, the voice is still not inspiring and gentle.
- In addition, when reading sports news, with specialized sports terms, readers cannot read these words correctly. For example, in football, to pronounce the number “0” instead of 2-0 (two nil), the pronunciation pattern is (two zero); In tennis, instead of 30-0 (thirty love), the pronunciation pattern is (thirty zero).
