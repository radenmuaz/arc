# arc
```
TEXT=train1
cd arc
python3 cprepare_arc.py  --times 10 --name ../datasets/$TEXT   --hue  --rotate --shuffle-train --flip --truncate
cd ../fairseq
fairseq-preprocess --source-lang src --target-lang tgt --trainpref ../datasets/$TEXT/train --validpref ../datasets/$TEXT/valid --testpref ../datasets/$TEXT/valid --destdir data-bin/$TEXT
NAME=a1
TEXT=train1
fairseq-train data-bin/$TEXT  --max-source-positions 9000 --max-target-positions 9000  --save-dir chkpts/$NAME --batch-size 4  --optimizer adam --lr 1e-3 --lr-scheduler inverse_sqrt --warmup-updates 5000 --no-epoch-checkpoints --arch arclc-e

```
python vprepare_arc.py  --times 50 --name ../datasets/arcfv4    --hue   --shuffle-train --rotate --flip  --truncate --repeat-frames --stretch

fairseq-generate data-bin/arcfv3 --max-source-positions 9000 --max-target-positions 9000     --path fchkpts/$NAME/checkpoint_last.pt --batch-size 1 --beam 20  --nbest 3 --gen-subset valid --print-alignment 

