# DeepKSL

Ubuntu / MacOS

1. Darknet build

$ git clone https://github.com/dasolhwang/DeepKSL

$ cd DeepKSL

$ nano Makefile

    GPU=0
    CUDNN=0
    OPENCV=0
    
$ make

$ wget https://pjreddie.com/media/files/yolov3.weights

2. Customize Darknet
Image dataset directory : '/darknet/data/img/'
Image bounding box coordinates : '/darknet/data/img/'

train image directory list(train.txt) : '/darknet/data/'  
test image directory list(test.txt) : '/darknet/data/' 

yolo-obj.cfg 
- 각자의 class 수에 맞게 마지막 filters 수정 필요 
    
        filters = (classes수 + 5) * 5

- ex) class = 1 인 경우, 마지막 filters = 30

obj.data

    classes = 1 (수정)
    train  = /data/train.txt
    valid  = /data/test.txt
    names = /data/obj.names
    backup = backup/

obj.names
- 자신의 class label을 정의해준다
- ex) 손을 찾는 모델인 경우
        
        hand
        
- ex) 개와 고양이를 찾는 모델인 경우 
        
        dog
        cat


3. train
학습된 weight는 backup/에 100단위로 저장

        ./darknet detector train data/obj.data yolo-obj.cfg yolov3.weights
        ./darknet detector train {.data} {.cfg} {.weights default}

  
4. test
3000번 돌아간 weight가 저장되었다면(yolo-obj_3000.weights)

        ./darknet detector demo test data/obj.data yolo-obj.cfg backup/yolo-obj_3000.weights test.mp4
        ./darknet detector demo test data/obj.data yolo-obj.cfg backup/yolo-obj_3000.weights data/img/image.jpg       
        ./darknet detector demo test {.data} {.cfg} {.weights} {데모하고 싶은 이미지 혹은 영상}        

