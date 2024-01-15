---
layout: post
title: Passive Acoustic Monitoring
image: 
  path: /assets/img/projects/bird_favicon.jpg
accent_image: 
  background: '#FADC19'
  overlay: false
accent_color: '#ccc'
theme_color: '#ccc'
description: >
  Passive Acoustic Monitoring allows researchers to get in-depth biodiversity data faster than ever before.
invert_sidebar: true
---

## Passive Acoustic Monitoring


* toc
{:toc}


## Overview
Soundscapes are an essential part of the natural world and the ecosystems that make it up. 
Healthy, diverse soundscapes correlate with healthy, diverse ecosystems.
By deploying audio recorders in the field, researchers, conservationists, and wildlife 
enthusiasts can tap into the wealth of information propagating through the air in the 
form of sound. Passive acoustic monitoring involves the sampling, processing, and analysis 
of ecological soundscapes, usually with a focus on specific wildlife species. 


## Why passive acoustic monitoring?
Traditional field surveys--using human observers--can be costly and resource-intensive.
Surveyors need to be trained by experts and then brought to often remote locations. 
Because we cannot feasibly leave multiple people stationed continuously across a landscape, 
remote sensing technology offers attractive alternatives. Wildlife cameras, drones, and other
optical solutions can only go so far: line of sight is often more challenging to establish 
than line of hearing. 

Imagine a dense forest, a foggy seaside, or any where at night. Sound propagates through such 
obstrucitons much more easily. What's more, audio data takes up less storage. Since animals
often vocalize in a way that is unique to their species, the captured audio signatures provide 
the means for comprehensive biodiversity assessments. 

## Why the bird focus?
The simple answer: they are everywhere and they sing!

Birds—being one of the more conspicuous and extensively studied groups of animals around 
the world—can often serve as indicators of underlying environmental 
health(Lovette & Fitzpatrick, 2016). If a healthy and diverse population of birds is 
present and thriving, it generally means that the landscape is in good shape. The image 
of ‘the canary in the coal mine’ is commonly evoked to explain birds’ role as important 
bioindicators.

So, when we see that North American birds have experienced a nearly 30% decline since 
1970—a net loss of roughly three billion birds (Rosenberg et al.,2019)—it sends a clear 
signal that a crisis is underway. 

The crisis is not limited to the avian world: the global Living Planet Index—which is 
measured by monitoring over 20,000 wildlife populations of roughly 4,400 species across 
all classes of vertebrates indicates an overall decline in average abundance of 68% between 
1970 and 2016 (Almond et al., 2020). These widespread, rapid declines pose an immense 
challenge to conservationists seeking to preserve diverse wildlife communities and 
the landscapes upon which they depend.

Since birds are are highly vocal and present in nearly all terrestrial ecosystems, they
provide a crucial glimpse into what is going on and can point to dangers ahead. And since
each species of bird vocalizes in a unique way, it is possible to train machine learning 
models to analyze audio and identify the species present within it.

## Major Benefits
### Greater survey coverage
This applies to both time and space. Remote recording units can be deployed across entire 
landscapes and can record over long periods of time. It is much easier to scale up survey 
efforts when not reliant on expert observers being physically present in the field.

### Detecting rare, elusive, and cryptic species
With continuous recording schedules, your odds of capturing those few, scattered vocalizations 
of an elusive target increase dramatically. Since conservation efforts often aim to protect
species that are becoming locally rare or endangered, researchers need new methods like this
to improve detection rates.

### Non-invasive
There is no disturbance to the environment or to the animals, ensuring minimal impact and quality data.
Often, surveys rely on trapping, luring, or some other distrubance-dependent method. While these are
tried-and-true and can be professionaly executed with minimal harm, non-invasive methods are generally
preferable. Also, surveying wildlife without a human being skulking around might offer a better
glimpse into their their true behavior.

### Reproducible methods
Using recorders and automated processing methods makes acoustic surveys more consistent over time, 
letting us compare surveys from different times and different projects much more effectively. Just like
human beings, automated processes make mistakes. Unlike human beings, however, they make the mistakes
the exact same way every time, making it more likely that a rise or fall observed in the occupancy of a 
certain species reflects the underlying biological reality rather than a major difference in 
observation/detection methods. 

### A soundscape museum
Bioacoustic monitoring creates a museum-style specimen of an ecological soundscape at a given time.  
This data can be revisited and analyzed multiple times, helping you find things you may have missed.
You can also revisit the same, intact dataset with  new questions or new tools in the future, similar 
to the way animal specimens in museum collections can be revisited with novel genetic analysis methods 
decades later.

### Cost effective
One of the more expensive aspects of wildlife monitoring getting a team of trained professionals out into 
sometimes remote locations, multiple times.  Acoustic monitoring allows you to purchase a lot more survey 
coverage with the same amount of funding. 


Most elements now have rounded borders, making the design 
look more modern (dare I say "Stripe-ified") than ever before. 

### Lower effort, greater reward
To survey an entire preserve or landscape can be arduous work. With acoustic monitoring, a single field 
technician carrying a backpack full of audio recorders can cast a wide net over the landscape. With a data
processing pipeline powered by artificial intelligence to handle the rest, conservationists can greatly
improve the capacity of their monitoring efforts. 

## Data Processing
To take advantage of these benefits requires detection models and data management solutions to be in place.
You cannot simply collect 1,000 hours of audio and hope to listen to it all for the animal you seek! For a 
long time, no machine learning models were accurate or efficient enough to make acoustic monitoring viable
at large scales. However, recent advances in artificial intelligience--particularly the advent of convolutional 
neural networks--have resulted in a quantum leap in terms of what is now possible. I talk more about these
powerful detection models in this post, 
[Deep Learning for Audio Classification of Wildlife Vocalizations](/blog/bioacoustics/deep learning/2024-01-13-deep_learning_for_audio_classification_of_wildlife_vocalizations){:.heading.flip-title}, 
in case you like to know more.

## Conclusion
We have got to act quickly when it comes to biodiversity conservation. All too often, in the time that it 
takes to generate a scientific report, the issue has already progressed catastrophically. Acoustic monitoring
is one of many forms of conservation tech that are emerging out of the AI boom with great potential for 
supporting positive change. 
