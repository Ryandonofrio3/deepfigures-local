
**Issue: Currently getting the docker container set up but seems that there is no module named rect? I can see in vendor/tensorboxresnet/tensorboxresnet/utils that Stitch_wrapper.pyx is calling rect.py not sure why it wouldnt be found?**


PS C:\Users\donofrio\Documents\GitHub\deepfigures-open> python .\manage.py detectfigures .\output\ .\test1.pdf
2023-10-25 18:02:36,342:INFO:scripts.build:Executing: docker build --tag deepfigures-cpu:0.0.1 --file C:\Users\donofrio\Documents\GitHub\deepfigures-open\dockerfiles/cpu/Dockerfile .      
[+] Building 2.8s (23/23) FINISHED                                             docker:default
 => [internal] load .dockerignore                                                        0.0s
 => => transferring context: 167B                                                        0.0s 
 => [internal] load build definition from Dockerfile                                     0.0s 
 => => transferring dockerfile: 1.47kB                                                   0.0s 
 => [internal] load metadata for docker.io/tensorflow/tensorflow:1.15.0-py3              0.4s 
 => [ 1/18] FROM docker.io/tensorflow/tensorflow:1.15.0-py3@sha256:ac8457b32f65b68ee242  0.0s
 => [internal] load build context                                                        0.0s 
 => => transferring context: 9.26kB                                                      0.0s 
 => CACHED [ 2/18] RUN apt-get update --fix-missing     && apt-get install -y     git    0.0s 
 => CACHED [ 3/18] RUN git clone https://github.com/jasperproject/jasper-client.git jas  0.0s 
 => CACHED [ 4/18] WORKDIR /work                                                         0.0s 
 => CACHED [ 5/18] ADD ./requirements.txt /work                                          0.0s 
 => CACHED [ 6/18] RUN pip3 install --upgrade pip     && pip install Cython==0.25.2      0.0s 
 => CACHED [ 7/18] RUN pip3 install --upgrade Cython                                     0.0s 
 => CACHED [ 8/18] RUN pip3 install fastparquet                                          0.0s 
 => CACHED [ 9/18] RUN pip3 install -r ./requirements.txt                                0.0s 
 => CACHED [10/18] RUN pip3 install --upgrade beautifulsoup4                             0.0s 
 => CACHED [11/18] ADD ./vendor/tensorboxresnet /work/vendor/tensorboxresnet             0.0s 
 => CACHED [12/18] RUN pip3 install -e /work/vendor/tensorboxresnet                      0.0s 
 => CACHED [13/18] RUN pip3 install tensorflow==1.15                                     0.0s 
 => CACHED [14/18] RUN pip3 install scipy==1.0.1                                         0.0s 
 => CACHED [15/18] RUN pip3 install pdf2image                                            0.0s 
 => CACHED [16/18] RUN apt-get install -y python-poppler                                 0.0s 
 => CACHED [17/18] ADD . /work                                                           0.0s
 => [18/18] RUN pip3 install --quiet -e /work                                            2.2s 
 => exporting to image                                                                   0.1s 
 => => exporting layers                                                                  0.1s 
 => => writing image sha256:1af73592d028b2452b5c69d36c30222fd20414ebe063a5eb8e331a16daf  0.0s 
 => => naming to docker.io/library/deepfigures-cpu:0.0.1                                 0.0s 

What's Next?
  1. Sign in to your Docker account → docker login
  2. View a summary of image vulnerabilities and recommendations → docker scout quickview     
2023-10-25 18:02:39,791:INFO:scripts.detectfigures:Executing: docker run --rm --env-file deepfigures-local.env --volume C:\Users\donofrio\Documents\GitHub\deepfigures-open\output:/work/host-output --volume C:\Users\donofrio\Documents\GitHub\deepfigures-open:/work/host-input deepfigures-cpu:0.0.1 python3 /work/scripts/rundetection.py   /work/host-output   /work/host-input/test1.pdf
WARNING:tensorflow:
The TensorFlow contrib module will not be included in TensorFlow 2.0.
For more information, please see:
  * https://github.com/tensorflow/community/blob/master/rfcs/20180907-contrib-sunset.md       
  * https://github.com/tensorflow/addons
  * https://github.com/tensorflow/io (for I/O related ops)
If you depend on functionality not listed there, please file an issue.

Traceback (most recent call last):
  File "/work/scripts/rundetection.py", line 37, in <module>
    rundetection()
  File "/usr/local/lib/python3.6/dist-packages/click/core.py", line 1128, in __call__
    return self.main(*args, **kwargs)
  File "/usr/local/lib/python3.6/dist-packages/click/core.py", line 1053, in main
    rv = self.invoke(ctx)
  File "/usr/local/lib/python3.6/dist-packages/click/core.py", line 1395, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/usr/local/lib/python3.6/dist-packages/click/core.py", line 754, in invoke
    return __callback(*args, **kwargs)
  File "/work/scripts/rundetection.py", line 29, in rundetection
    from deepfigures.extraction import pipeline
  File "/work/deepfigures/extraction/pipeline.py", line 16, in <module>
    from deepfigures.extraction import (
  File "/work/deepfigures/extraction/detection.py", line 14, in <module>
    from deepfigures.extraction import (
  File "/work/deepfigures/extraction/tensorbox_fourchannel.py", line 28, in <module>
    from tensorboxresnet import train
  File "/work/vendor/tensorboxresnet/tensorboxresnet/train.py", line 27, in <module>
    from tensorboxresnet.utils import train_utils, googlenet_load, tf_concat
  File "/work/vendor/tensorboxresnet/tensorboxresnet/utils/train_utils.py", line 17, in <module>
    from tensorboxresnet.utils.stitch_wrapper import stitch_rects
  File "tensorboxresnet/utils/stitch_wrapper.pyx", line 3, in init tensorboxresnet.utils.stitch_wrapper
ModuleNotFoundError: No module named 'rect'
Traceback (most recent call last):
  File "C:\Users\donofrio\Documents\GitHub\deepfigures-open\manage.py", line 72, in <module>  
    manage()
  File "C:\Users\donofrio\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.10_qbz5n2kfra8p0\LocalCache\local-packages\Python310\site-packages\click\core.py", line 1130, in __call__
    return self.main(*args, **kwargs)
  File "C:\Users\donofrio\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.10_qbz5n2kfra8p0\LocalCache\local-packages\Python310\site-packages\click\core.py", line 1055, in main    
    rv = self.invoke(ctx)
  File "C:\Users\donofrio\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.10_qbz5n2kfra8p0\LocalCache\local-packages\Python310\site-packages\click\core.py", line 1657, in invoke  
    return _process_result(sub_ctx.command.invoke(sub_ctx))
  File "C:\Users\donofrio\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.10_qbz5n2kfra8p0\LocalCache\local-packages\Python310\site-packages\click\core.py", line 1404, in invoke  
    return ctx.invoke(self.callback, **ctx.params)
  File "C:\Users\donofrio\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.10_qbz5n2kfra8p0\LocalCache\local-packages\Python310\site-packages\click\core.py", line 760, in invoke   
    return __callback(*args, **kwargs)
  File "C:\Users\donofrio\Documents\GitHub\deepfigures-open\scripts\detectfigures.py", line 60, in detectfigures
    execute(
  File "C:\Users\donofrio\Documents\GitHub\deepfigures-open\scripts\__init__.py", line 52, in execute
    raise subprocess.CalledProcessError(
subprocess.CalledProcessError: Command 'docker run --rm --env-file deepfigures-local.env --volume C:\Users\donofrio\Documents\GitHub\deepfigures-open\output:/work/host-output --volume C:\Users\donofrio\Documents\GitHub\deepfigures-open:/work/host-input deepfigures-cpu:0.0.1 python3 /work/scripts/rundetection.py   /work/host-output   /work/host-input/test1.pdf' returned non-zero exit status 1.
