---
title: "Creating a Notebook Service in Fabric"
date: 2026-04-09T14:33:00+01:00
draft: false
---

## Fabric Notebook Service

In Fabric, you can write Python using Notebooks in pipelines to retrieve data from external systems where they may be too complex or not supported by any of the available connectors in a dataflow. For example, you can use a notebook to recursively call a paginated endpoint until there is no data left. You can do something similar using the activities within a pipeline as well but I have found notebooks to be more adaptable and extensible. Deciding which to use can ultimately depend upon who will be consuming and maintaining the Fabric instance.

Part of Fabric that has irked me coming from a .NET background with a lot of options for testing, is that it is difficult to prove what I've got works without having to run pipelines and dataflows.

To make a testable notebook you can create a notebook 'Service' that behaves as a central area for other notebooks to connect to and use. This is a Notebook but structured as a class that means we can use the magic '% Run' command in another notebook and to run the methods within it.

This is an example of a service notebook:

![Notebook service class](/images/fabricnotebookservice.jpg)

And here is how you would use it:

![Notebook service class usage](/images/fabricnotebookservice2.jpg)

If you want to test the create_id_dataframe method for example, you can supply it a different value as the retrieved_ids parameter.