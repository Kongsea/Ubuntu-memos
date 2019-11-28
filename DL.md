# Record tips using Deep Learning

## 1. Use [Maskrcnn-benchmark](./https://github.com/facebookresearch/maskrcnn-benchmark)

   - Train on multi-GPU
      ```
      export NGPUS=4
      CUDA_VISIBLE_DEVICES=0,1,2,3 python -m torch.distributed.launch --nproc_per_node=$NGPUS tools/train_net.py --config-file "path/to/config/file.yaml"
      ```
   - Multi-task trained on multi-GPU
      The first task can be trained as above. When you want to launch the second task, it will raised error.
      You can launch it through adding `--master_port 12345`
      ```
      export NGPUS=4
      CUDA_VISIBLE_DEVICES=4,5,6,7 python -m torch.distributed.launch --master_port 12345 --nproc_per_node=$NGPUS tools/train_net.py --config-file "path/to/config/file.yaml"
      ```