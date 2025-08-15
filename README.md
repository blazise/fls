快手抖音网红爆料网站大全视频免费观看


        CHECK(cudaEventRecord(stop));
        CHECK(cudaEventSynchronize(stop));
        float elapsed_time;
        CHECK(cudaEventElapsedTime(&elapsed_time, start, stop));

        if (repeat > 0)
        {
            t_sum += elapsed_time;
            t2_sum += elapsed_time * elapsed_time;
        }

        CHECK(cudaEventDestroy(start));
        CHECK(cudaEventDestroy(stop));
    }

    const float t_ave = t_sum / NUM_REPEATS;
    const float t_err = sqrt(t2_sum / NUM_REPEATS - t_ave * t_ave);
    printf("%d %g\n", num, t_ave);
}


5 流回调

流回调是一种特别的技术，有点像是事件的函数，这个回调函数被放入流中，当其前面的任务都完成了，就会调用这个函数，但是比较特殊的是，在回调函数中，需要遵守下面的规则

    回调函数中不可以调用CUDA的API
