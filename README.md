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
--crop-dim 224


python scripts/train_classifier.py \
--input-dir output/intermediate \
--model-path  model/20170511-185253/20170511-185253.pb \
--classifier-path output/classifier.pkl \
--num-threads 16 \
--num-epochs 25 \
--min-num-images-per-class 2 \
--is-train 


