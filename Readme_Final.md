## 實作流程

1.下載OWOD-master文件夾
2. 在 OWOD 內部建立 Detectron2: 
   ```
   python -m pip install 'git+https://github.com/facebookresearch/detectron2.git
   ```
3. 根據自身設備狀況調整GPU版本
4. 進行設備環境的完善(不同設備需要進行不同的環境調整):
   ```
    pip install reliability
    pip install shortuuid
   ```
5. 進入OWOD-master文件夾，建立VOC2007文件夾
6. 在VOC2007文件夾中分別建立Annotations、ImageSets、JPEGImages文件夾 
7. 在Annotations文件夾下存入相應資料的所有xml檔案
![image1](https://github.com/ysq0917/YZU_Final_Project/blob/main/image1.png)


8. 在ImageSets文件夾下建立Main文件夾，在其中存入所有資料名稱的txt檔案 txt 檔案內部:
![image2](https://github.com/ysq0917/YZU_Final_Project/blob/main/image2.png)


9.在JPEGImages文件夾下存入所有待訓練的影像資料
![image3](https://github.com/ysq0917/YZU_Final_Project/blob/main/image3.png)


10. 開 啟 "/OWOD/detectron2/data/datasets" 路 徑 下 的 pascal_voc.py 檔 案 ， 將 VOC_CLASS_NAMES、T2_CLASS_NAMES 內的種類改為自己資料集的種類
![image4](https://github.com/ysq0917/YZU_Final_Project/blob/main/image4.png)


11. 開啟"/OWOD/configs/OWOD/t1/"路徑下的 t1_train.yaml 檔案
![image5](https://github.com/ysq0917/YZU_Final_Project/blob/main/image5.png)

 我們將 R-50.pkl 作為第一階段的訓練基底模型，並根據自身資料數量設定 STEPS 與 MAX_ITER，根據自身需要調整文件夾位置。本階段訓練的數量通過 CUR_INTRODUCED_CLS 設定。

12. 進入環境與文件夾後輸入以下指令進行模型第一階段訓練，並修改調整GPU、config file、batch size
  ```
  python tools/train.net.py --num-qpus 4 -config-file <change to the appropriate config file> SOLVER.IMS_PER_BATCH 4 SOVER.BASE_LR 0.005
  
  ```
13. 模型訓練結束後，到自己的路徑下查看相應的模型 (model_final.pth)與測試結果(log.txt)
14. 使用類似方式進行下一階段訓練，開啟/configs/OWOD/t2/"路徑下的 t2_train.yaml
![image6](https://github.com/ysq0917/YZU_Final_Project/blob/main/image6.png)
 
 


 
