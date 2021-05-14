이 프로젝트가 추정하는 거리는 정확하지 않습니다. 

yolov5를 이용하여 제 스스로 작성해본 것입니다. 

x, y, w, h 값을 이용하여 대상의 거리를 추정하는 다른 더 좋은 코드가 있을 것입니다.

결과는 아래와 같습니다. 

![image](https://user-images.githubusercontent.com/20491139/118228457-2f4c0400-b4c5-11eb-9ca6-272464f983e7.png)


코드의 내용을 설명하자면, 

detect.py 를 통해 Custom detect object를 한 다음에, x, y, w, h 좌표를 이용해서 거리를 추정했습니다. 

절대로 정확하지 않습니다. 저는 차후 값을 보정하여 사용할 계획입니다. 

detect.py에서 수정한 코드는 아래와 같습니다. 

```
if save_img or opt.save_crop or view_img:  # Add bbox to image
    c = int(cls)  # integer class
    label = None if opt.hide_labels else (names[c] if opt.hide_conf else f'{x_top:.2f} {y_top:.2f} {width:.2f} {height:.2f}')
    distancei = (2 * 31.4 * 180) / (width + height) * 10
    label2 = f'{names[0]} {distancei:.1f}cm'
    #print(label2, distancei)
    plot_one_box(xyxy, im0, label=f'{distancei:.1f}cm', color=colors(c, True), line_thickness=1)
    #cv2.putText(frame, str(label2), (x_top,y_top+5), cv2.FONT_HERSHEY_SIMPLEX, 0.5, colors(c, True),2)
    if opt.save_crop:
        save_one_box(xyxy, imc, file=save_dir / 'crops' / names[c] / f'{p.stem}.jpg', BGR=True)
```
