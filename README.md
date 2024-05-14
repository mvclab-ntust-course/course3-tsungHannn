[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/X3WkcXtG)

# 執行方式
使用學長給的教學:
https://huggingface.co/docs/diffusers/en/training/lora

## 參數
```bash
accelerate launch --mixed_precision="bf16" examples/text_to_image/train_text_to_image_lora.py   --pretrained_model_name_or_path="runwayml/stable-diffusion-v1-5"  --train_data_dir="data_dir/"   --dataloader_num_workers=0   --resolution=512 --center_crop --random_flip   --train_batch_size=1   --gradient_accumulation_steps=4   --max_train_steps=500   --learning_rate=1e-02   --max_grad_norm=1   --lr_scheduler="cosine" --lr_warmup_steps=0   --output_dir="result/"   --report_to=wandb   --checkpointing_steps=10   --validation_prompt="Patrick is standing beside the rock."   --seed=1337
```
因為跑的時間不多，所以把max_train_steps設定較少(500)，learning rage設定較大(0.02)

## 訓練資料
diffusers/data_dir\
用派大星的圖片作為訓練資料\
![image](https://github.com/mvclab-ntust-course/course3-tsungHannn/assets/85086644/446f76cc-872a-4fbc-9968-1f2d73a641f7)


**Train on NVIDIA 3060 for 13 hours, 100 Epoch.**\
Use GPU Memory 11.7 GB (95%)\
![image-2](https://github.com/mvclab-ntust-course/course3-tsungHannn/assets/85086644/c8e5bde2-9a55-4488-b5fa-91e2d52e993f)



**但是最後訓練失敗，原因應該是派大星被系統擋住了**
![image-1](https://github.com/mvclab-ntust-course/course3-tsungHannn/assets/85086644/de9ebc3f-f713-459b-bf1f-70c88cef6cc3)


原本一開始訓練得不錯，有看出model想要趨近派大星
![image-3](https://github.com/mvclab-ntust-course/course3-tsungHannn/assets/85086644/adab6233-9f55-4077-a308-6dd1a548fc65)


但是被NSFW擋住之後感覺整個訓練就掛掉了

第4個Epoch開始出現全黑圖片，第5個Epoch就開始出現整張單一顏色的圖片了
![image-4](https://github.com/mvclab-ntust-course/course3-tsungHannn/assets/85086644/1f2ba070-5b84-4657-b428-2deec94ae376)


第五個Epoch
![image-5](https://github.com/mvclab-ntust-course/course3-tsungHannn/assets/85086644/80e3ddbb-ebf1-4125-b479-04fe6b5e9ce7)


Train完100個Epoch已經很晚了，電腦太吵只能關掉了。

結果產不出派大星，我甚至找不到可以迴避掉系統的Token
![image-6](https://github.com/mvclab-ntust-course/course3-tsungHannn/assets/85086644/40f87f6e-39fd-4db0-b7ab-643b8a1e64d8)
