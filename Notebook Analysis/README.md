1. At In[5], 'mask' was defined as pixel where perspective transformed image is not 0. (For obastacle perception)
2. At In[6], rock_thresh function was defined to threshold rock samples. To find rock samples default threshold was set as R>110, G>110, B<50.
   To check, rock_threshed = rock_thresh(rock_img) was executed and the result was successful.
3. At In[9], overall image proccessing step is executed in funtion 'process_image'.
    
    rock = rock_thresh(warped, rgb_thresh=(110, 110, 50)) <br />
    colorsel = color_thresh(warped, rgb_thresh=(160, 160, 160)) <br />
    obstacle = np.absolute(np.float32(colorsel)-1)*mask<br />
    
    Above functions are executed to threshold rock, navigatable terrain, obstacles. Obstacles are defined as where perspective transformed pixel is not 0 and colorsel is 0(Innavigatable terrain).

    warped_thresh[:,:,1]=rock*255 <br />
    warped_thresh[:,:,2]=colorsel*255 <br />
    warped_thresh[:,:,0]=obstacle*255 <br />
    
    Rock samples are colored as green, navigatable terrain as blue, obstacles as red.
    
    obstacle_xpix, obstacle_ypix = rover_coords(obstacle) <br />
    rock_xpix, rock_ypix = rover_coords(rock) <br />
    xpix, ypix = rover_coords(colorsel) <br />
    
    Then images are converted to rover coordinate.
    
     obstacle_x_world, obstacle_y_world = pix_to_world(obstacle_xpix, obstacle_ypix, data.xpos[data.count],data.ypos[data.count], data.yaw[data.count], data.worldmap.shape[0], scale) <br />
     rock_x_world, rock_y_world = pix_to_world(rock_xpix, rock_ypix, data.xpos[data.count],data.ypos[data.count], data.yaw[data.count], data.worldmap.shape[0], scale) <br />
     x_world, y_world = pix_to_world(xpix, ypix, data.xpos[data.count],data.ypos[data.count], data.yaw[data.count], data.worldmap.shape[0], scale) <br />
     
     Then to world cocordinate to make worldmap. data.xpos[data.count],data.ypos[data.count],data.yaw[data.count] was used to figure out rover's position and orientation.

    data.worldmap[rock_y_world,rock_x_world,:] = 255 <br />
    data.worldmap[y_world,x_world,2] = 255 <br />
    data.worldmap[obstacle_y_world,obstacle_x_world,0] = 255 <br />
    
    Rock samples are marked as white, navigatable terrain as blue and obstacle as red.
    
