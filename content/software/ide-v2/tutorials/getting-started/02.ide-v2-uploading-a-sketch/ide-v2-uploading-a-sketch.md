---
title: 'How to upload a sketch with the Arduino IDE 2.0'
difficulty: easy
description: 'Learn the basics of verifying and uploading sketches with the new IDE 2.0.'
tags:
 - Uploading
 - Basics
author: 'Karl Söderby'
---

## How to Upload a Sketch with the Arduino IDE 2.0

In the Arduino environment, we write **sketches** that can be uploaded to Arduino boards. In this tutorial, we will go through how to select a board connected to your computer, and how to upload a sketch to that board, using the Arduino IDE 2.0.

You can easily download the editor from the [Arduino Software page](https://www.arduino.cc/en/software#experimental-software). 

You can also follow the [downloading and installing the Arduino IDE 2.0](./ide-v2-downloading-and-installing) tutorial for more detailed guide on how to install the editor.

### Requirements

- Arduino IDE 2.0 installed. 

### Verify VS Upload

There are two main tools when uploading a sketch to a board: **verify** and **upload.** The verify tool simply goes through your sketch, checks for errors and compiles it. The upload tool does the same, but when it finishes compiling the code, it also uploads it to the board.

A good practice is to use the verifying tool before attempting to upload anything. This is a quick way of spotting any errors in your code, so you can fix them before actually uploading the code. 

### Uploading a Sketch

Installing a core is quick and easy, but let's take a look at what we need to do. 

**1.** Open the Arduino IDE 2.0. 

**2.** With the editor open, let's take a look at the navigation bar at the top. At the very left, there is a **checkmark** and an **arrow pointing right**. The checkmark is used to **verify**, and the arrow is used to **upload.** 

![Verifying and uploading buttons.](assets/uploading-a-sketch-img01.png)

**3.** Click on the verify tool (checkmark). Since we are verifying an empty sketch, we can be sure it is going to compile. After a few seconds, we can see the result of the action in the console (black box in the bottom). 

![Successful compilation printed in the console.](assets/uploading-a-sketch-img02.png)

**4.** Now we know that our code is compiled, and that it is working. Now, before we can upload the code to our board, we will first need to select the board that we are using. We can do this by navigating to **Tools > Port > {Board}**. The board(s) that are connected to your computer should appear here, and we need to select it by clicking it. In this case, our board is displayed as **COM44 (Arduino UNO)**.

![Selecting the board.](assets/uploading-a-sketch-img03.png)

**5.** With the board selected, we are good to go! Click on the **upload** button, and it will start uploading the sketch to the board. 

**6.** When it is finished, it will notify you in the console log. Of course, sometimes there are some complications when uploading, and these errors will be listed here as well.

![Successful upload printed in the console.](assets/uploading-a-sketch-img04.png)

Congratulations, you have now uploaded a sketch to your Arduino board!

