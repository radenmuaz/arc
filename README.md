# arc
```
TEXT=arct1
NAME=a1
cd arc
python cprepare_arc.py  --times 30 --name ../datasets/$TEXT   --hue  --rotate --shuffle-train --flip --truncate
cd ../fairseq
fairseq-preprocess --source-lang src --target-lang tgt --trainpref ../datasets/$TEXT/train --validpref ../datasets/$TEXT/valid --testpref ../datasets/$TEXT/valid --destdir data-bin/$TEXT
fairseq-train data-bin/$TEXT  --max-source-positions 9000 --max-target-positions 9000  --save-dir fchkpts/$NAME --batch-size 16  --optimizer adam --lr 1e-3 --lr-scheduler inverse_sqrt --warmup-updates 5000 --no-epoch-checkpoints --arch arclc-c
```
python vprepare_arc.py  --times 50 --name ../datasets/arcfv4    --hue   --shuffle-train --rotate --flip  --truncate --repeat-frames --stretch

fairseq-generate data-bin/arcfv3 --max-source-positions 9000 --max-target-positions 9000     --path fchkpts/$NAME/checkpoint_last.pt --batch-size 1 --beam 20  --nbest 3 --gen-subset valid --print-alignment 
