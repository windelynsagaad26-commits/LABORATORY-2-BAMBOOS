# Plant-Species-Image-Classification

##### B. Plant Species Section
#### Common Name: Dwarf Bamboo

![00007_beautifulbam_e70ad3f5361d](https://github.com/user-attachments/assets/f9eb7870-0b84-4026-a60d-a3d6f37a2367)

Scientific Name: Bambusa spp. (or possibly Pleioblastus spp., depending on the exact type)
Description:
The plant shown is a Dwarf Bamboo, a smaller and more compact variety of bamboo. It grows in dense clumps with multiple thin, green stems and narrow, pointed leaves. Compared to larger bamboo species, dwarf bamboo is shorter in height but still maintains the same fast-growing nature. It is commonly used for landscaping, garden decoration, and ground cover due to its thick and bushy appearance. Dwarf bamboo thrives in warm environments and prefers moist soil, often growing well near water or shaded areas..


<img width="814" height="1000" alt="00003_myplantin_14e23d9014ca" src="https://github.com/user-attachments/assets/57a80684-dcfb-4dc8-b511-83c57fb53201" />
Scientific Name: Bambusa or Phyllostachys species (various)

Description: "Arrow bamboo" historically refers to any of several small to medium-sized, straight-stemmed bamboo species used by indigenous peoples (including Native Americans and East Asian cultures) to make arrows. The common requirements include: straight, hollow internodes, a hard outer rind, and sufficient rigidity to withstand the force of a bow. In the United States, native species like Arundinaria gigantea (River Cane) were commonly used.




#### C. Model Training Details

Train the Model<img width="1915" height="1094" alt="Screenshot 2026-03-30 120932" src="https://github.com/user-attachments/assets/653c2ea7-2b8d-4861-8427-17f65ceaca70" />
### 


 #### Epochs

<img width="145" height="299" alt="Screenshot 2026-03-30 133419" src="https://github.com/user-attachments/assets/36b5788e-8276-4c6f-bb67-5462afb27054" />



 #### Batch Size

<img width="145" height="299" alt="Screenshot 2026-03-30 133419" src="https://github.com/user-attachments/assets/e162b44e-e8a2-4c0b-b426-a0a208a05245" />

 ###### Learning Rate

<img width="145" height="299" alt="Screenshot 2026-03-30 133419" src="https://github.com/user-attachments/assets/a532ec75-ba83-4ef0-8308-14ae9c06ab8b" />
 

###  Collect “Under the Hood” Results



##### D. Model Evaluation

#### Confusion Matrix

<img width="348" height="260" alt="Screenshot 2026-03-30 131931" src="https://github.com/user-attachments/assets/39b43099-ae40-41d4-8c30-c61f42866109" />

##### Accuracy per class
<img width="351" height="248" alt="Screenshot 2026-03-30 131947" src="https://github.com/user-attachments/assets/a078c834-50e2-4f87-a65e-a6cd98cf5d07" />


###### Overall accuracy

<img width="333" height="985" alt="Screenshot 2026-03-30 132033" src="https://github.com/user-attachments/assets/afada765-1284-4367-bf4f-d54c969b36aa" />


#####  Loss values (if available)

<img width="314" height="909" alt="Screenshot 2026-03-30 132201" src="https://github.com/user-attachments/assets/6c2e9008-f87d-4420-8f29-5eb903a42e41" />

###### E. Model Testing
Embedded 10 testing screenshots from the Preview section

<img width="251" height="937" alt="Screenshot 2026-03-30 132628" src="https://github.com/user-attachments/assets/33ff76e2-9ac3-4f24-926e-07d94c136676" /> <img width="247" height="938" alt="Screenshot 2026-03-30 132557" src="https://github.com/user-attachments/assets/1b581e7a-a1d1-4af3-b6a9-8193df6dc576" /><img width="238" height="939" alt="Screenshot 2026-03-30 132537" src="https://github.com/user-attachments/assets/fa25f51e-e157-463a-b3dd-f34ff702cf0d" />
<img width="249" height="940" alt="Screenshot 2026-03-30 132513" src="https://github.com/user-attachments/assets/4a67fe98-3023-4c99-bf78-74b63bfca919" /><img width="185" height="714" alt="Screenshot 2026-03-30 133103" src="https://github.com/user-attachments/assets/c1a5e6cc-ea5c-4ead-bd40-cab8ae5863df" /><img width="185" height="467" alt="Screenshot 2026-03-30 133027" src="https://github.com/user-attachments/assets/e4c6109e-5fb2-4859-abe4-2ffee56c66f5" />
<img width="190" height="483" alt="Screenshot 2026-03-30 132942" src="https://github.com/user-attachments/assets/001a9604-ce62-4369-9ba3-cbb1a87aa34d" />
<img width="186" height="708" alt="Screenshot 2026-03-30 132916" src="https://github.com/user-attachments/assets/f52862c4-33b8-4ca8-9f24-6de199d26fcc" />
<img width="188" height="479" alt="Screenshot 2026-03-30 132846" src="https://github.com/user-attachments/assets/c7ebe7f7-cf5e-4a3e-9a45-3cf4758d7477" /><img width="188" height="899" alt="Screenshot 2026-03-30 132800" src="https://github.com/user-attachments/assets/c1ed33b4-0177-4514-ba9d-92d20751953e" /><img width="184" height="717" alt="Screenshot 2026-03-30 132741" src="https://github.com/user-attachments/assets/90e8e7af-0342-4060-bd7e-a59596b87952" /><img width="248" height="938" alt="Screenshot 2026-03-30 132657" src="https://github.com/user-attachments/assets/5257826b-a037-4ec0-933e-5c6609d76be8" />



###### Reflection Questions:

1. How did the number of images per class affect your model’s accuracy?

More images per class made the model more accurate because it had more examples to learn from.

2. Which plant species were most commonly misclassified and why?

Plants with similar leaves or appearance were often misclassified because they look alike.

3. How did changing the epochs, batch size, or learning rate affect the training results?

More epochs improved accuracy, but too much can overfit. Learning rate and batch size affected how fast and stable the training was.

4. What challenges did you encounter during dataset collection and labeling?

It was hard to find many clear images and avoid duplicates. Organizing the images was also challenging.

5. If you were to improve your model, what specific changes would you make and why?

I would add more images, use better quality images, and adjust the training settings to improve accuracy.
