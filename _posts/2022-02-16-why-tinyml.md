---
title: "Bringing deep learning models to microcontrollers"
date: 2022-02-16T18:47:00.000Z
lang: de
categories:
  - blog
tags:
  - tinyML
---

Deep learning models owe their initial success to massively parallel processing on GPU clusters with lots of memory. The models grew more extensive and complex, requiring virtually unlimited computational and energy resources. Today, only a few wealthy technology companies can afford this expense.

In recent years, however, this hunger for resources has also led to machine learning models for terminals with severely limited resources. These models, known as tinyML, are suitable for limited memory and computing power devices, where Internet connectivity is either non-existent or limited.

How does tinyML fit into a world where machine learning algorithms are becoming more comprehensive and resource-intensive?

Machine learning models have grown exponentially in recent years - from less than 100 *million* parameters to 175 *billion* parameters from 2017 to 2020!

Moreover, they consume more energy than ever before. According to one estimate, the carbon footprint of a *single training* of BERT (a recently developed natural language processing model ) is enough to fly back and forth between New York and San Francisco.

Clearly, training and deploying modern machine learning algorithms require significant resources. As a result, most modern machine learning algorithms are deployed on relatively powerful devices and typically have access to the cloud, where most of the resource-intensive computation occurs.

Although current Deep Learning models are very successful, they are not applicable in all situations, for example, areas with poor Internet connectivity, such as drone rescue missions, or where data privacy regulations are high, such as in healthcare. 
These requirements have made on-device ML attractive, both scientifically and commercially. Your iPhone now runs on-device face and voice recognition. Your Android phone can do an on-device translation. Your Apple Watch uses machine learning to recognize motion and ECG patterns.

These ML models have become more compact, computationally, and memory-efficient in the last years. But their use has also been made possible by advances in hardware. Our smartphones and wearables now have more computing power than a server did 30 years ago. Some even have dedicated co-processors for ML inference.

TinyML takes this a step further by enabling deep learning models to run on microcontrollers (MCUs), which are even more resource-efficient than the tiny computers we carry in our pockets and on our wrists.

Microcontrollers are not new in themselves - there are an estimated 250 billion microcontrollers in use today - and they are integral to the growing presence of the *Internet-of-Things* (IoT). They are tiny, sometimes on the order of *a few millimeters*. They are cheap, with average selling prices below $0.50. They do not have an operating system. They have a small CPU, are limited to a few hundred kilobytes of low-power memory (SRAM) and a few megabytes of storage, and have no networking equipment. They consume extremely little power, on the order of *a few milliwatts*, and can run for years on coin cell batteries.

Since most of the analysis in tinyML systems is performed directly on the microcontrollers - *in the field* or *at the edge* - the results are available *instantly*. This can be very useful in situations where *low latency* is essential - for example, in fast-moving warning systems - where potential delays in accessing cloud servers are problematic.

## Application areas

Let's take a closer look at some often-cited use cases for tinyML.

### Industrial predictive maintenance

Early detection (prediction) of wear and tear in production lines and industrial plants in remote or hard-to-access locations.

A concrete solution based on an intelligent microcontroller has been developed by [Australian StartUp Ping](https://pingmonitor.co) for remote wind turbines. Ping's tinyML microcontrollers (part of their IoT framework) continuously and autonomously monitor turbine performance using embedded algorithms. The cloud is accessed only for summary data and only when needed.
This has improved Ping's ability to alert turbine operators to potential problems before they become serious.

### Agriculture

Identifying pests and diseases on crops in remote areas.

In Africa, the cassava crop is a vital food source for hundreds of millions of people each year. However, it is under constant attack from a variety of diseases.

To combat this, PlantVillage, an open-source project at Penn State University, has developed an AI-driven app called [*Nuru*](https://play.google.com/store/apps/details?id=plantvillage.nuru) that can work on cell phones without Internet access - an important consideration for remote African farmers.

The Nuru app has successfully countering threats to the cassava crop by analyzing sensory data in the field.

As the next step in Nuru's development, PlantVillage plans to more fully utilize tinyML and deploy microcontroller sensors on remote farms to provide better tracking data for analysis.

### Healthcare

Hackaday, an open-source hardware collaboration, uses its Solar Scare Mosquito System to combat mosquito-borne diseases such as malaria, dengue fever, and the Zika virus.

The system works by moving standing water in tanks and swamps, denying mosquito larvae the opportunity to grow (larvae need standing water to survive).

The water is moved by small robotic platforms that operate only when needed (saving energy) by analyzing rain and acoustic sensor data. Summary statistics and alerts (to warn of mass mosquito breeding events) are sent using low-power, low-bandwidth protocols.

### Other

Researchers at the Polytechnic University of Catalonia have used tinyML *to reduce* fatal collisions with elephants* on the Siliguri-Jalpaiguri railroad line in India. There have been over 200 such crashes in the last 10 years. The researchers designed a *solar-powered acoustic and thermal sensing system* with embedded machine learning as an early warning system.

TinyML is being deployed in waters around Seattle and Vancouver *to reduce* the risk of whale attacks in* busy shipping lanes. Arrays of sensors with embedded machine learning perform *continuous, real-time monitoring* and send alerts to ships when whales are in their vicinity.

## Outlook

So while conventional machine learning is evolving toward more complex and resource-intensive systems, tinyML is filling a growing need at the other -smaller- end of the spectrum. Importantly, it does so in a sustainable way - *with low latency, low power, and minimal connectivity requirements*. As a result, you get a variety of low-cost, easy-to-use intelligent applications.

Like many other trends, tinyML has some famous advocates:

[Harvard Associate Professor Vijay Janapa Reddi](https://scholar.harvard.edu/vijay-janapa-reddi/classes/cs249r-tinyml), a leading researcher and practitioner in tinyML, believes that tinyML will become deeply embedded in everyday life in the coming years and is, therefore, a real opportunity for anyone who wants to learn about it and get involved.

Also excited is [Pete Warden](https://petewarden.com), former Google research engineer and technical lead of TensorFlow Lite, a software framework for implementing tinyML models. Warden believes that tinyML *will impact almost every industry in the future* such as retail, healthcare, agriculture, fitness, and manufacturing. The following statement from him is interesting:

"It's obvious that there is a huge untapped market waiting to be tapped with the right technology. We need something that works with cheap microcontrollers, uses very little energy, is based on computation rather than radio, and can turn all our wasted sensor data into something useful. That's the gap that machine learning, especially Deep Learning, is filling."

It's exciting to keep track of where AI - applications are headed and what other possibilities it offers. However, it is already safe to say that intelligent microcontrollers (tinyML) have set the sights of AI research on more resource-efficient - and therefore environmentally friendly - solutions. If the result is simple solutions that are affordable for everyone, we have already gained a lot.
