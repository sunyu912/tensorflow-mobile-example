# Overview

0. Run Docker in your Mac
1. Open the terminal

2. Downlaod the project workspace. Run:

`git clone https://github.com/sunyu912/tensorflow-mobile-example.git`

If you see errors on not recognizing `git`, you need to install Git first. Please see https://git-scm.com/book/en/v2/Getting-Started-Installing-Git

3. 

`cd tensorflow-mobile-example/`

4. Copy your trained tf_files:

`cp -r ~/tf_files .`

5. Run Docker environment:

`docker run -it \
  --publish 6006:6006 \
  --volume ${HOME}/tensorflow-mobile-example:/tensorflow-mobile-example \
  --workdir /tensorflow-mobile-example \
  tensorflow/tensorflow:1.1.0 bash`
  
6. Verify the tool and model prediction works:

`python scripts/label_image.py tf_files/flower_photos/daisy/21652746_cc379e0eea_m.jpg tf_files/retrained_graph.pb`

If you can see the following output, that means the tool has been installed correctly:

Elapsed time: 0.643202

daisy (score = 0.99779)
sunflowers (score = 0.00153)
dandelion (score = 0.00046)
tulips (score = 0.00016)
roses (score = 0.00006)

7. Optimze the model for mobile:

`python -m tensorflow.python.tools.optimize_for_inference \
  --input=tf_files/retrained_graph.pb \
  --output=tf_files/optimized_graph.pb \
  --input_names="Cast" \
  --output_names="final_result"`
  
8. Copy the optimized models to mobile Android projecT:

`cp tf_files/optimized_graph.pb android/assets/retrained_graph.pb`
`cp tf_files/retrained_labels.txt android/assets/`

9. Open Android Studio (Please install it first at https://developer.android.com/studio/index.html

10. Import an existing Android project. Please choose the `android` folder in the `tensorflow-mobile-example` folder.
