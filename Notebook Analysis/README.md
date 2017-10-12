1. At In[5], 'mask' was defined as pixel where perspective transformed image is not 0. (For obastacle perception)
2. At In[6], rock_thresh function was defined to threshold rock samples. To find rock samples default threshold was set as R>110, G>110, B<50.
   To check, rock_threshed = rock_thresh(rock_img) was executed and the result was successful.
3. At In[9], overall image proccessing step is executed in funtion 'process_image'.
    
    rock = rock_thresh(warped, rgb_thresh=(110, 110, 50))
    colorsel = color_thresh(warped, rgb_thresh=(160, 160, 160))
    obstacle = np.absolute(np.float32(colorsel)-1)*mask
