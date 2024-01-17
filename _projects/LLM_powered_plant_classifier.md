---
layout: project
title: 'Developing an LLM-powered plant classifier using LangChain'
caption: Tool to classify plants as native or alien in certain countries based solely  on extracted context from Wikipedia
description: >
  Tool to classify plants as native or alien in certain countries based solely  on extracted context from Wikipedia
date: 17 January 2024
image: 
  path: /assets/img/projects/LLM_plant_graphic.png
#   srcset: 
#     1920w: /assets/img/projects/VIRA.jpg
#     960w:  /assets/img/projects/qwtel@0,5x.jpg
#     480w:  /assets/img/projects/qwtel@0,25x.jpg
links:
  - title: Link
    url: https://github.com/johannesnelson/LLM_Botanist
accent_color: '#4fb1ba'
accent_image: 
  background: '#193747'
theme_color: '#193747'
sitemap: false
---
### Developing an LLM-Powered Plant Classifier Using LangChain

* toc
{:toc}

## Demo App
For demonstration purposes and ease-of-use, I made a runnable app that I am hosting on Streamlit. You can see how it
works by entering your own info as text, a CSV, or you can simply run the demo built into the app. The app can 
also be [accessed on Streamlit](https://llm-botanist.streamlit.app/).


<style>
.responsive-iframe-container {
  position: relative;
  padding-bottom: 56.25%; /* 16:9 Aspect Ratio */
  padding-top: 25px;
  height: 0;
}
.responsive-iframe-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>

<div class="responsive-iframe-container">
  <iframe src="https://llm-botanist.streamlit.app/" frameborder="0"></iframe>
</div>
<br>

## Overview/Background
### Reason for Development
During my work as a data scienctist/consultant for Conservation International, the monitoring team
expressed interest in being able to automatically classify plants as native, alien, or invasive in certain landscapes. The
size and geogrpahic distribution of their restoration portfolio made this a challenge--there was a lot of data coming in from dozens
of countries around the world.

### Obstacles/First Attempts
I began with the more pressing issue of automatically identifying potential invasive species in the 
dataset. Because of their potentially harmful effects on ecosystems, it was easy to find a centralized,
global list of invasive species. Using a combination of techniques, I was able to develop a tool to 
rapidly parse the dataset for potential invasive species. I talk more about this tool here: 
[Detecting Invasive Flora: Leveraging Web Scraping and API Integration with Biodiversity Databases](/projects/invasives_scanner){:.heading.flip-title}.

No such centralized database tracking a plant's status as alien or native in various global regions exists (or at least
I could not find it!). Certain geographical regions had databases tracking native plants--such as the USA and Europe--but
with a portfolio of restoration projects covering countries like Madagascar, Brazil, the Saudi Arabia, and the Philippines (to name 
a few), it quickly became apparent that another strategy was necessary. Even if I could locate a database that covered each region,
incorporating each of these programatically into an automated pipeline would have been a major hurdle.

To start off, I decided at least to script a semi-automated workflow that a human user could execute within R Studio wihtout having to 
search for and consult external resources. This work flow, which I talk about more in another 
post--[Data Analysis Pipeline for a Global Tree Restoration Portfolio](/projects/PPC_data_analysis_pipeline){:.heading.flip-title}--
presents the user with extracted and filtered wikipedia text as well as a map plotting 1,000 points of occurence data, color-coded
to indicate whether the data included tags of 'alien' or 'native'. This workflow works well, and seriously cuts down on the 
time required to process large datasets. But it still bothered me that it wasn't fully automated.

### Idea for new approach
Since the above workflow sucecessfully found relevant wikipedia info for most of the species, and since this info more often then
not contained explicit information about native and alien ranges, I thought that a Large Language Model (LLM), guided by clear
prompts and incorporated into the processing workflow might be able to parse this context accurately--applying labels to the dataset
under the hood and saving a human annotator a lot of time.

## Development
To develop this LLM-powered classifier, I moved from R over to Python because of my familiarity with frameworks like LangChain--a library
that facilitates the inclusion of LLMs into regular Python workflows. The first challenge was in developing prompts to get the job done. 
Casual use of models like ChatGPT involves simple discussions which can iteratively get closer to what you desire. For this, however, since
it would all be occuring on the back-end, I needed the outputs of the model to be in a format that I could manipulate reliably with code (like JSON).
So, I began numerous experiements with prompt-engineering to see what would work best. 

### Prompt Engineering
Including natural language into a scripted workflow is a novel, exciting, and frustrating experience. Normally when we code something, 
we know what is going to happen. Executing code is a clear, deterministic process that, given the same input, will always result in the
same output. Not so with language models.

The term prompt engineering is in some senses very accurate--I had to develop systematic schemas and format instructions for the model to produce
an accurate output that could be appended to a dataframe. In other ways, though, it ignores the part of the process that feels a lot more
like creating magical incantations or trying to sternly guide a disobedient child to follow clear instructions. 

#### Obstacles/First Attempts
My first experiments were quite simple. A general prompt assigned the LLM its role, and attempted--all within the same schema--to instruct
it in how to make decisions. Some of the key points were as follows:
* You are a botanical assistant, helping scientists classify a plant as native or alien given a species name and a country name
* You will be provided context from Wikipedia, and this is the *only* source of information you may use when making a decision. If
there is no context, you must classify the plant as 'unknown'
* You must output your decision in JSON

These early approaches worked in some cases, but output was erratic: sometimes the model used outside context when deciding; sometimes
the model would call a plant alien in a certain country even though the context was clear about it being native simply because later
parts of the context focused on its being widely introduced elsewhere; and outputs were sometimes well formed, but occasionally missing
key formatting components that would trip up any output parser downstream.
#### Response Schemas
LangChain offers ways to engineer prompts using **response schemas**. These structure and standardize the way a language model 
interprets and responds to user input. These basically help break down the language model's task on the interpretation side, and 
also guide the model in creating outputs that adhere to a strict structure that can be easily parsed in the next stage of the workflow. 
Using this approach allowed me to more easily get consistently structured outputs, and also allowed me to break down and address areas
where the reasoning or behavior of the model was not as expected.

Often, LLMs struggle with tasks that require somewhat complex reasoning, so my inital attempt at making the model classify a plant
in a single step was bound to fail. Giving the model 'space and time to think' improves performance greatly. What I mean by this 
is explicitly break down the reasoning steps, having the model produce intermediate outputs, which it can then use to make a final 
decision. So, rather than: 'classify these plants with this context', the multi-step prompt (simplified) sounded more like this:

1.) First, restate the species name and the country under review.

2.) If there is no context provided, your decision must be 'unknown'.

3.) If there is context provided, try to extract the native range from this context.

4.) Then, try to extract the alien range from the context.

5.) Then, using the information about the ranges that you extracted, detail your steps 
of reasoning that lead you to your final decision.

6.) Record your final decision.


The response schemas in LangChain make breaking this down easy. These responses get passed to a built-in output parser
that integrates format instructions into the output. The below were not the only schemas I used, but they provide a good
idea for how they work. The 'name' argument provides that structured output label, and the description is a discrete prompt
that is used to create the value to which that label is assigned. 

```python
native_range_schema = ResponseSchema(name="native_range",
                                    description= "From the context provided, ascertain the native range of the plant species, and write it here. "
                                    "If there is no clear native range given in the context, state: unable to ascertain native range from provided " 
                                    "context. This should be a single string.")

alien_range_schema = ResponseSchema(name="alien_range",
                                    description= "From the context provided, ascertain the alien range of the plant species, and write it here. "
                                    " There may not be mention of an alien or introduced range, in which case you should simply state: unable 
                                    " to ascertain alien range. This should be a single string.")

reasoning_schema = ResponseSchema(name="reasoning",
                                    description= "Based upon the native range and alien range that you extracted, explain the reasoning that leads "
                                    "to your decision about the specific country under review. Remember that the country name may not be explicitly mentioned "
                                    "but that it might exist within the broader continental or regional boundaries that are provided. Explain your reasoning "
                                    "clearly about this. If you first identify it as native because of the extracted range, then stick to that decision. "
                                    "This should be a single string.")
    
```

### Conclusion
After numerous iterations, I settled on a series of prompts and a workflow and had a working classifier and succesfully processed
over 2,000 species country combinations. As with any classification process, results should be validated before they are used to inform action
(especially considering the non-deterministic nature of LLMs and their tendency to hallucinate), but validating a pre-labelled dataset
that includes the wikipedia context and reasoning steps will be a lot more efficient than working from scratch. 

I embedded the app above, which you can test out by entering a species and a country manunally or by inputting a CSV with a
column for 'species' and a column for 'country'.