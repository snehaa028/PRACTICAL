SMA Practical Codes 
## 1. Study various SMA tools  
1. Go to https://communalytic.org/  
2. Sign In (clg account) and create New Project then Add dataset then add Youtube API key 
AIzaSyAfFegeZ_ALsLcpHN5IWwMkXXaRCSeyLLM 
3. Paste any yt video url link and done
   
## 2. Data Collection for Social Media Platform 
from yt_dlp import YoutubeDL 
import pandas as pd 
with YoutubeDL({"quiet": True}) as y: 
r = y.extract_info("ytsearch20:Laptop Review", download=False) 
data = [[v["title"], v["uploader"], v["view_count"], 
v["like_count"], v["comment_count"], 
v["upload_date"], v["duration"], v["webpage_url"]] 
for v in r["entries"]] 
df = pd.DataFrame(data, columns=[ 
"Title","Channel","Views","Likes", 
"Comments","Upload Date","Duration","URL" 
]) 
df.to_csv("youtube_business_data.csv", index=False) 
print(df.head()) 

## 3. Data Cleaning & Storage of Social Media Data 
from cleantext import clean 
import pandas as pd 
from pymongo import MongoClient 
df = pd.DataFrame({ 
"user":["john_doe","alice_99","mike_123","sara_k"], 
"tweet":[ 
"I love AI!!! #MachineLearning http://example.com", 
"Worst service ever!!! #badexperience", 
"Python is awesome :) #coding #AI", 
"Delivery was late and bad #fail" 
], 
"location":["Mumbai","Delhi",None,"Pune"] 
}) 
df["cleaned_tweet"] = df["tweet"].apply(clean)   # fixed (no wrong params) 
df["location"] = df["location"].fillna("Unknown") 
col = MongoClient("mongodb://localhost:27017/")["social_media_db"]["cleaned_posts"] 
col.delete_many({}) 
col.insert_many(df[["user","cleaned_tweet","location"]].to_dict("records")) 
print(df) 

## 4. Exploratory Data Analysis with visualization 
import pandas as pd 
import seaborn as sns 
import matplotlib.pyplot as plt 
# Simplest Data Dictionary 
data = { 
"Channel": ["TechHub", "GadgetBox", "ReviewPro", "ByteSize", "TechHub"], 
"Views": [10000, 50000, 25000, 5000, 15000], 
"Likes": [500, 2000, 1200, 100, 800], 
"Comments": [50, 150, 80, 10, 60] 
} 
df = pd.DataFrame(data) 
# Calculate Metric 
df['Engagement %'] = (df['Likes'] + df['Comments']) / df['Views'] * 100 
# Fast Plotting 
plt.figure(figsize=(10, 4)) 
# Plot A: Engagement Rate by Channel 
plt.subplot(1, 2, 1) 
sns.barplot(x="Engagement %", y="Channel", data=df, estimator="mean") 
# Plot B: Correlations 
plt.subplot(1, 2, 2) 
sns.heatmap(df.select_dtypes('number').corr(), annot=True, cbar=False) 
plt.tight_layout(); plt.show() 

## 5. Content based social media analysis 
import pandas as pd, matplotlib.pyplot as plt 
from textblob import TextBlob 
from wordcloud import WordCloud 
from collections import Counter 
# Simple Data 
data = ["I love this laptop!      
", "Bad screen"] 
", "Terrible battery life         
df = pd.DataFrame(data, columns=["Content"]) 
# Shortest Sentiment & Keyword Logic 
", "Normal build quality", "Amazing speed! 
df["Pol"] = df["Content"].apply(lambda t: TextBlob(t).sentiment.polarity) 
df["Sent"] = df["Pol"].apply(lambda p: "Pos" if p > 0 else ("Neg" if p < 0 else "Neu")) 
words = " ".join(data).lower().split() 
# Print Summary 
print(df[["Content", "Sent"]], "\nTop Words:", Counter(words).most_common(3)) 
# Quick Visuals 
f
ig, (ax1, ax2) = plt.subplots(1, 2, figsize=(10, 4)) 
df["Sent"].value_counts().plot(kind="pie", ax=ax1, title="Sentiment") 
ax2.imshow(WordCloud(background_color="white").generate(" ".join(words))) 
ax2.axis("off") 
plt.show() 

## 6. Structure based Social Media Analysis Model 
import pandas as pd, networkx as nx, matplotlib.pyplot as plt, community as louvain 
# Data & Graph 
df = pd.DataFrame({'s':['A','A','B','B','C','C','D','E','F','G','H','D','B'], 
't':['B','C','C','D','D','E','E','F','G','H','A','G','H']}) 
G = nx.from_pandas_edgelist(df, 's', 't') 
# Analysis 
part = louvain.best_partition(G) 
rank = nx.pagerank(G) 
# Quick Visual & Output 
nx.draw(G, with_labels=True, node_color=list(part.values()), cmap='Set3') 
plt.show() 
print("Communities:", part) 
print("Top User:", max(rank, key=rank.get)) 

## 7. Dashboard & reporting tool on real tie social media data 
https://github.com/Atharva12072004/X-Social-Media-Data-Analysis 
run .pbix file in Power BI 

## 8. Design Creative Content for promotion of Your Business On Social Media 
Go to Canva and create one post for promotion  

## 9. Analyse competitor activities using Social Media Data 
import pandas as pd 
import seaborn as sns 
import matplotlib.pyplot as plt 
# Competitor Data (Brand vs Competitor A & B) 
data = { 
'Brand': ['You', 'Comp_A', 'Comp_B'], 
'Followers': [10000, 50000, 15000], 
'Total_Engage': [1200, 2000, 1800] # Likes + Comments 
} 
df = pd.DataFrame(data) 
# Competitor Metric: Engagement Rate (True Influence) 
df['Eng_Rate %'] = (df['Total_Engage'] / df['Followers']) * 100 
# Quick Visual Battle 
sns.barplot(x='Brand', y='Eng_Rate %', data=df, palette='magma') 
plt.title("Who is Winning the Audience?") 
plt.show() 
print(df.sort_values('Eng_Rate %', ascending=False)) 

## 10. Social Media text analysis model 
import pandas as pd, matplotlib.pyplot as plt 
from textblob import TextBlob 
from collections import Counter 
# Simple Data (Posts) 
posts = ["I love this product", "Bad service", "Great price!", "Very slow delivery", "Amazing 
experience"] 
# Analyze: Sentiment (Positive/Negative) & Word Count 
sentiment = ["Positive" if TextBlob(p).polarity > 0 else "Negative" for p in posts] 
words = Counter(" ".join(posts).lower().split()).most_common(3) 
# Quick Visual & Output 
pd.Series(sentiment).value_counts().plot(kind='bar', color=['green', 'red']) 
plt.title("Text Sentiment Analysis"); plt.show() 
print(f"Sentiment: {sentiment}\nTop Topics: {words}")
