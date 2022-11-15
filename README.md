# Rasa Chatbot to perform movie search

* https://medium.com/betacom/building-a-rasa-chatbot-to-perform-movie-search-60cea9829e60
* https://medium.com/betacom/unsupervised-nlp-task-in-python-with-doc2vec-da1f7727857d

#### Fetch Dataset

* Download dataset from:
https://www.kaggle.com/datasets/jrobischon/wikipedia-movie-plots
* Copy to server
```
scp -i ~/ec2-keyfile.pem /Users/x/Downloads/wiki_movie_plots_deduped.csv ubuntu@<IP_ADDRESS>:/home/ubuntu/chatbot_movies/datasets/wiki_movie_plots_deduped.csv
```

#### Fetch or Build Model 

* Download from https://drive.google.com/u/0/uc?id=1R0ERc4IcuZqosg43w2_E93dmt6rPX7cp&export=download
* Copy to server after creting relevant folder
```
scp -i ~/code/ec2-keyfile.pem /Users/x/Downloads/doc2vec_model_movies.zip ubuntu@<IP_ADDRESS>:/home/ubuntu/chatbot_movies/models_doc2vec/doc2vec_model_movies.zip
```
* Unzip on the server
```
sudo apt install unzip
unzip -l doc2vec_model_movies.zip

unzip doc2vec_model_movies.zip -d models_doc2vec/
```

scp -i ~/code/ec2-keyfile.pem /Users/cuttlefish/Downloads/doc2vec_model_movies.zip ubuntu@3.25.191.196:/home/ubuntu/chatbot_movies/doc2vec_model_movies.zip

* OR Build
    * https://medium.com/betacom/unsupervised-nlp-task-in-python-with-doc2vec-da1f7727857d
    * https://radimrehurek.com/gensim/models/doc2vec.html
    * https://radimrehurek.com/gensim/auto_examples/tutorials/run_doc2vec_lee.html#sphx-glr-auto-examples-tutorials-run-doc2vec-lee-py

#### Install Python 3

* Install Python 3
```
pyenv install -l
pyenv install 3.9.15
```

#### Install Dependencies

* Add dependencies. See .python-version for compatible version
```
pyenv local 3.9.15
pyenv shell 3.9.15
pip install -U pip
pip install -r requirements.txt
pip install rasa
```

### Train & Interact

```
rasa train
tmux
sudo kill -9 $(lsof -t -i:5005 -sTCP:LISTEN);
sudo kill -9 $(lsof -t -i:5055 -sTCP:LISTEN);
rasa run actions
rasa shell
rasa interactive
```

### Experiment

* Enter the following to get a response
```
--> Your input
hi
...
great
...
yes
...
Jedi knight lightsaber starship
```
