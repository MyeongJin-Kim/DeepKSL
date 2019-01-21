
# DeepKSL

[![Video](http://img.youtube.com/vi/mfdXBcDYc1A/0.jpg)](https://www.youtube.com/watch?v=mfdXBcDYc1A)
  
  
Ubuntu, MacOS
  
### Darknet build  

```
git clone https://github.com/dasolhwang/DeepKSL
cd DeepKSL        
```

GPU, CUDNN, OPENCV 사용여부에 따라 설정 바꾸기 (사용하면 1,  사용하지 않으면 0)
```
nano Makefile
```
    # GPU, CUDNN, OPENCV 사용여부
    GPU=0 
    CUDNN=0

    
  
### Customize Darknet

- /darknet/data/img/ : 해당 경로에 Image dataset과 Image bounding box coordinates 두기
  
- /darknet/data/train.txt
- /darknet/data/text.txt
  
  
[ yolo-obj.cfg ]
  
        filters = (classes수 + 5) * 5
  
- 각자의 class 수에 맞게 마지막 filters 수정 필요 
- ex) class = 1 인 경우, 마지막 filters = 30
  
  
[ obj.data ]

    classes = 1
    train  = /data/train.txt
    valid  = /data/test.txt
    names = /data/obj.names
    backup = backup/
    
- classes = 클래스 수
  
  
[ obj.names ]
        
        dog
        cat
        
  
- 자신의 class label을 정의해준다        
- ex) 개와 고양이를 찾는 모델인 경우 
  
  
### train
  
yolo-v3의 초기 weight 다운받기
```
wget https://pjreddie.com/media/files/yolov3.weights 
```
  
pre-trained weight를 가지고 detection 모델 학습
```
./darknet detector train data/obj.data yolo-obj.cfg yolov3.weights  
```
  
- 학습된 weight는 backup/에 100단위로 저장
- ./darknet detector train [.data] [.cfg] [.weights default]
    
  
### test/demo
```
./darknet detector demo test data/obj.data yolo-obj.cfg backup/yolo-obj_3000.weights test.mp4
./darknet detector demo test data/obj.data yolo-obj.cfg backup/yolo-obj_3000.weights data/img/image.jpg   
```
  
- 3000번 돌아간 weight가 저장되었다면(yolo-obj_3000.weights)
- ./darknet detector demo test [.data] [.cfg] [.weights] [데모하고 싶은 이미지 혹은 영상]        
   
