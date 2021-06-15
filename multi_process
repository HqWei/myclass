import argparse
import json
import os
from multiprocessing import Process

from tqdm import tqdm


def cp_imgs(img_root,img_list,target_dir):

    for line in tqdm(img_list):
        file=os.path.join(img_root,line.rstrip())
        save_file=os.path.join(target_dir,line.rstrip().split("/")[-1])
        os.system(f"cp {file} {save_file}")


def main():

    tmp_list="tmp_dir.lst"
    target_dir="tmp_dir"
    img_root="TMP"
    with open(tmp_list) as f:
        lines=f.readlines()
        total_num=len(lines)
    kernel=4
    ps = []
    for pid in range(kernel):
        st = total_num * pid // kernel
        ed = total_num * (pid + 1) // kernel
        sub_item_list = lines[st:ed]
        sub_out_file = os.path.join(target_dir,str(pid))
        if not os.path.exists(os.path.join(sub_out_file)):
            os.makedirs(sub_out_file)
        p = Process(
            target=cp_imgs,
            args=(img_root, sub_item_list, sub_out_file))
        p.daemon = True
        p.start()
        ps.append(p)

    for p in ps:
        p.join()

    print('finish')


if __name__ == '__main__':
    main()
