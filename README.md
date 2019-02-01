# tensorflow_face_detect

Intstallation :
 downloads $ wget -O dlib-19.4.tar.bz2 http://dlib.net/files/dlib-19.4.tar.bz2 \
    && tar -vxjf dlib-19.4.tar.bz2
	
	downloads $  \
	 cd dlib-19.4    \
	 && cd examples    \
	 && mkdir build    \
	 && cd build     \
	 && cmake ..     \
	 && cmake --build . --config Release
	
	downloads/dlib-19.4$make all
	
	downloads/dlib-19.4$ python setup.py install

Commands:	
python scripts/download_and_extract_model.py \
--model-dir model

python scripts/preprocess.py \
--input-dir data \
--output-dir output/intermediate \
--crop-dim 128


python scripts/train_classifier.py \
--input-dir output/intermediate \
--model-path  model/20170511-185253/20170511-185253.pb \
--classifier-path output/classifier.pkl \
--num-threads 6 \
--num-epochs 25 \
--min-num-images-per-class 2 \
--is-train 
=================================tensorflow command======================
=======
IMAGE_SIZE=224
IMAGE_SIZE=128
ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}"

ARCHITECTURE="mobilenet_1.0_${IMAGE_SIZE}"

====================V1 version=========================================
ARCHITECTURE="mobilenet_1.0_${IMAGE_SIZE}"
python -m scripts.retrain  \
--bottleneck_dir=face_tf_files/bottlenecks \
--how_many_training_steps=5000 \
--model_dir=face_tf_files/models/ \
--summaries_dir=face_tf_files/training_summaries/"${ARCHITECTURE}" \
--output_graph=face_tf_files/retrained_graph.pb \
--output_labels=face_tf_files/retrained_labels.txt \
--architecture="${ARCHITECTURE}" \
--image_dir=face_tf_files/face_photos



python -m tensorflow.python.tools.optimize_for_inference \
  --input=face_tf_files/retrained_graph.pb \
  --output=face_tf_files/optimized_graph.pb \
  --input_names="input" \
  --output_names="final_result"

  
  python -m scripts.label_image \
--graph=face_tf_files/optimized_graph.pb \
--labels=face_tf_files/retrained_labels.txt \
--image=
  
  python -m scripts.quantize_graph \
  --input=face_tf_files/optimized_graph.pb \
  --output=face_tf_files/rounded_graph.pb \
  --output_node_names=final_result \
  --mode=weights_rounded
  
  
  

