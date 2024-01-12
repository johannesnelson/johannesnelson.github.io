---
layout: project
title: 'RailNET'
caption: Exploring Deep Learning solutions for cryptic species monitoring
description: >
  Using Deep Learning to listen for elusive species like the Virginia rail.
date: 1 Jun 2020
image: 
  path: /assets/img/projects/VIRA.jpg
#   srcset: 
#     1920w: /assets/img/projects/VIRA.jpg
#     960w:  /assets/img/projects/qwtel@0,5x.jpg
#     480w:  /assets/img/projects/qwtel@0,25x.jpg
links:
  - title: Link
    url: https://github.com/johannesnelson/RailNET
accent_color: '#4fb1ba'
accent_image: 
  background: '#193747'
theme_color: '#193747'
sitemap: false
---
### RailNET - A deep learning approach to detecting elusive acoustic signals


* toc
{:toc}

## Overview
RailNET is an ensemble of Convolutional Neural Networks that specializes in a single bird: the Virginia rail.
Rails are cryptic marsh birds--meaning that they are exceedingly difficult to find with your eyes. Being secretive
and difficult to detect means that monitoring programs often struggle to gather data about population trends. 
Because their signals are rare and sporadic, and because one needs to detect these scattered signals from within
an audio dataset that is overwhelmingly comprised of sounds that are *not* from the target species, exploring
means for improving model performance in this use-case would be generalizable to other scenarios where 
massive class imbalance in the real-world data is unavoidable. 
## Model Development
### Why?
I developed RailNET because after joining an effort to study these birds using 
[Passive Acoustic Monitoring](/blog/2024-01-11-passive_acoustic_monitoring){:.heading.flip-title} on a 
large wetland preserve, I found that the existing state-of-the-art model for avian monitoring, BirdNET, 
was not performing as well as expected with the Virginia rail--spitting out thousands of false detections 
and missing a number of vocalizations I knew to be present. The precision of the model was hovering around just
1%. 

Sifting through a mountain of false positives in order to identify the true positives requires a lot of 
manual validation effort, so even small gains in model precision could drastically cut down on the hours 
required to process the data.

### Hypotheses
Before training, I had a few hypotheses for how I might improve upon BirdNET's performance--both model- and data-centric.

On the model side...
{:.lead}
* A specialist, binary-classsifer, might perform better on a specific species than a multi-class model
trained to recognize over 1,000, many of which are not relevant to the survey at hand.

* By ensembling multiple, separately trained ResNets, I could mitigate the impact of 
any single model's sometimes erratic predictions, potentially seeing a drop in false positives.

On the data side...
{:.lead}
* BirdNET was trained on publicly available data that is weakly labeled (i.e. the whole recordings have a
species label, but no timestamps indicating vocalizations). Since recordings are sure to be full of other
species vocalizing, there is a high risk of training data for a certain class being polluted with vocalizations
from another class. With automated methods to chop up recordings into training data samples, it is likely that 
the most prominent vocalizers in the avian community are the heaviest polluters and that infrequent vocalizers
like rails may often not even be the stars of their own recordings. By strongly labelling data for the Virginia 
rail (i.e. manually curating a class that *only* contains Virginia rail vocalizations), it is likely that 
performance will improve.

![Full-width image](/assets/img/projects/data_integrity.jpg)
This figure depicts two audio segments from a recording labelled in a public database as containing Virginia 
rail vocalizations, and illustrates the data integrity issue where multiple species can easily come to pollute
training data for a certain class. The navy blue boxes indicate true rail vocalizations, and the organge boxes
indicate the vocalizations of other species. In an automated, amplitude-based data curation process, these other
species would be included in the training data for the Virginia rail.
{:.figcaption}


* By excluding irrelevant species in training and focusing on species that are the most vocally gregarious, 
the model will be able to devote its full capacity to distinguishing between the Virginia rail's vocalizations
and the most likely background sounds.

### Model building and training
I built the models in Python using the PyTorch framework.


 Instead of a flashy sidebar image, I chose a solid background color.
However, I've given [certain](https://qwtel.com/projects/ducky-hunting/) [pages](https://qwtel.com/projects/blocky-blocks/) big sidebar images, and let Hydejack blend back to normal when the user navigates away.

While I love the font used for Hydejack's headings, for my personal site I felt less of a need to control the typesetting.
That's why I'm not using Google Fonts, and instead use whatever is the default for the reader's operating system.

```yml
google_fonts: false
font:         false
font_heading: false
font_code:    false
```

The configuration I use to enable the system font on my site. Feel free to copy!
{:.figcaption}
