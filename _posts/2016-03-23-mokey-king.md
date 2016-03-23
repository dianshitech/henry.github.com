---
layout: post
title:  php猴王问题
date:   2016-03-23
categories: php
excerpt: php猴王问题
---

* content
{:toc}

// 有 一群猴子排成一圈，按1,2,...,n依次编号。

// 然后从第1只开始数，数到第m只,把它踢出圈，从它后面再开始数， 再数到第m只，在把它踢出去...，

// 如此不停的进行下去， 直到最后只剩下一只猴子为止，那只猴子就叫做大王。

    public function findKingAction()
    {
        $m = 5;
        $n = 100;
        $monkey = range(1,$n); //构建猴子数组
        $i = 0;

        //遍历猴子数组
        while (list($k, $value) = each($monkey)){
            if (count($monkey) == 1){
                echo $value . "是猴王";
                exit();
            }

            if (++$i==$m){
               echo $monkey[$k] .'踢出去<br />';
               unset($monkey[$k]);  //把变量 清除
               $i = 0;                //指针归位
            }

            //如果已经数到最后的话  则继续进行下一轮的循环
            if (false === current($monkey)){
                reset($monkey);
            }
        }
    }