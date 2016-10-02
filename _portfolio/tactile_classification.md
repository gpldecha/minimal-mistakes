---
title: Syntouch tactile classifier
permalink: /projects/tactile_classifier/
excerpt: A tacticle classifier for the Syntouch artificial finger sensor.

header:
  teaser:  /projects/tactile_classifier/syntouch-th.jpg
  image:   /projects/tactile_classifier/syntouch.jpg
---


A developed a Qt-GUI and a set Machine Learning classifiers for the Syntouch BioTac sensor, a synthetic finger which
provide pressure and temperature information at 19 different locations across the finger's skin. Figure [Data collection](#syntouch_data)
illustrates the data gathering step for four different classes (<i>Corner, Edge, Surface, Air </i>). Once a sufficient
amount of data was gathered for each class I proceeded to learn different classifiers. I found that
Support Vector Machine (SVM) was the most robust classifier when compared with other classification approaches such as Gaussian Mixture Model.

<!-- BioTac Image -->
{% include image.html
            img="/projects/tactile_classifier/collecting_data_sensor.png"
            title="Data collection:"
            fig_id="syntouch_data"
            caption="Gathering training data for the different classes" %}
<br>
Figure [Syntouch BioTac classifier](#syntouch_v) illustratese the SVM classifier in action.


{% include yvideo.html id="h_Io_Tts3UI" width=560 height=315
                                        title = "Syntouch BioTac classifier"
                                        cap_id= "syntouch_v"
                                        caption = "Syntouch provides a 19 dimensional temporal signal. A classifier for <i>corner</i>, <i> edge </i>, <i> surface </i> and
                                        <i> air </i> was learned. The blue bars represent the probability the currently sensed data to be part of a class."
%}
