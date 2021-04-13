

<center><h1>RT-AK ֮ STM32</h1></center>

- [���](#���)
- [Ŀ¼�ṹ](#Ŀ¼�ṹ)
- [����˵��](#����˵��)
- [����](#����)
  - [1 ������������](#1������������)
  - [2 ָ����������](#2ָ����������)
- [�����б�](#�����б�)

## ���

*����Ŀ������ `RT-AK` ����Ŀ�е�һ����ģ�顣*

ʹ�� `STM32` ԭ��������п�����

- ԭ�������`X-CUBE-AI`
- ģ��֧�֣�`Keras | TFLite | Caffe | ONNX`

## Ŀ¼�ṹ

```shell
% tree -L 2 stm32 
stm32
������ backend_plugin_stm32
��?? ������ backend_cubeai.c
��?? ������ backend_cubeai.h
��?? ������ readme.md
������ config.py  # ���� `rt_ai_<model_name>_model.h` ��һЩ������Ϣ�������� <BSP>/applications
������ docs  # `X-CUBE-AI` ����ĵ�˵���� 
��?? ������ command_line_interface.html
��?? ������ embedded_client_api.html
��?? ������ en.stsw-link009.zip  # `STLink` ����
��?? ������ ...
��?? ������ relocatable.html
��?? ������ RT-AK֮STM32��������.md
��?? ������ stm32.c
��?? ������ stm32programmer-cli.pdf
��?? ������ ����(δ���).md
������ generate_rt_ai_model_h.py  # ���� `rt_ai_<model_name>_model.h` �������� <BSP>/applications
������ gen_rt_ai_model_c.py  # ���� `rt_ai_<model_name>_model.c` �������� <BSP>/applications
������ __init__.py
������ plugin_init.py  # �� `stm32ai` ��`X-CUBE-AI` ��ģ��ת�����ߣ���ӵ�ϵͳ����
������ plugin_stm32_parser.py  # `STM32` ƽ̨�����������Ĳ���
������ plugin_stm32.py  # `STM32` ƽ̨�������������
������ prepare_work.py  # ���������ļ��У���� x-cube-ai ��̬��� c-model �ļ�; ���ض�Ӧ�� Sconscript
������ README.md
������ run_x_cube_ai.py  # ���� `stm32ai` ���ߣ�����ģ��ת������
������ Sconscripts  # ģ��ת��֮�󣬲��뵽��Ŀ `scons` ����Ľű��ļ�
��?? ������ Middlewares
��?? ������ X-CUBE-AI
������ X-CUBE-AI.5.2.0  # `STM32Cube.AI` ���ṩ�ľ�̬��
    ������ Copyrights.txt
    ������ Middlewares
```

## ����˵��

> ��� `plugin_stm32_parser.py` 

| Parameter           | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| **`--ext_tools`**   | **`X-CUBE-AI` ���·����ģ��ת�����ߣ����� `stm32ai` ��ִ���������Ҫ�û�ָ��** |
| `--cube_ai`         | `X-CUBE-AI` ��������ľ�̬�⣬Ĭ��Ϊ`./platforms/stm32/X-CUBE-AI.5.2.0` |
| `--rt_ai_example`   | ���`rt_ai_<model_name>_model.c` ʾ���ļ���Ĭ���� `./platforms/stm32/docs` |
| `--stm_out`         | ���� `stm32ai` �̴߳���֮��������м��ļ���·����Ĭ���ǵ����ʱ������� |
| `--workspace`       | `stm32ai` ����ʱ��������ʱ��������Ĭ����`./stm32ai_ws`       |
| `--val_data`        | Ĭ��Ϊ�գ���ʹ���ڲ������ɵ�������ݼ��������û��Զ���������ݼ��� |
| `--compress`        | ��ʾ��Ӧ�õ�ȫ��ѹ�����ӣ���Ӧ����ȫ���Ӳ㣬��ѡ "1\|4\|8"��Ĭ��ֵ��`1` |
| `--batches`         | ָʾ�����˶����������������Ĭ����`10`                       |
| `--mode`            | "analyze\|validate" ģʽ����ѡ��+��generate��ģʽ�������У���`1`��ʾѡ�У���`{'001', '011', '101', '111'}`��ѡһ����Ĭ���� `001` |
| **--network**       | **�� `Documents` �е�ģ���ļ���ģ������Ĭ���� `mnist`**      |
| **--enable_rt_lib** | **�� `project/rtconfgi.h` �д򿪺궨�壬Ĭ���� `RT_AI_USE_CUBE`** |
| --clear              | �Ƿ���Ҫɾ�� `stm32ai` ���ɵ��м��ļ��� `stm_out` ��Ĭ��Ϊ`False` |

- ʾ����

  `--ext_tools="D:/Program Files (x86)/stm32ai-windows-5.2.0/windows"`

## ����

### 1 ������������

���� `edge-ai/RTAK/tools` ·�������иó���

![](https://gitee.com/lebhoryi/PicGoPictureBed/raw/master/img/20210223145923.png)

```shell
# ������������
python aitools.py --project=<your_project_path> --model=<your_model_path> --platform=stm32 --ext_tools=<your_x-cube-ai_path> --clear

# ʾ��
python aitools.py --project="D:\RT-ThreadStudio\workspace\test" --model="./Models/keras_mnist.h5" --platform=stm32 --ext_tools="D:\Program Files (x86)\stm32ai-windows-5.2.0\windows" --clear
```

![image-20210401181247394](https://gitee.com/lebhoryi/PicGoPictureBed/raw/master/img/20210401181248.png)

### 2 ָ����������

```shell
# ָ��ת��ģ�͵����ƣ�--model_name Ĭ��Ϊ network
python aitools.py --project=<your_project_path> --model=<your_model_path>  --model_name=<model_name>  --platform=stm32 --ext_tools=<your_x-cube-ai_path>

# �������� stm32ai �̹߳����в������ļ���--clear Ĭ��Ϊ��
# ������ڣ��򽫻�ɾ��`stm32ai` ����ʱ�����Ĺ����ļ��У���`--stm_out`
python aitools.py --project=<your_project_path> --model=<your_model_path> --platform=stm32 --ext_tools=<your_x-cube-ai_path>

# ָ������������־, --log Ĭ��Ϊ��
python aitools.py --project=<your_project_path> --model=<your_model_path> --log=./log.log --platform=stm32 --ext_tools=<your_x-cube-ai_path>

# ָ��������ļ������ƣ�--stm_out Ĭ���ǵ���ʱ�䣬���� './20210223'
python aitools.py --project=<your_project_path> --model=<your_model_path> --platform=stm32 --ext_tools=<your_x-cube-ai_path> --stm_out <new_dir>

# ָ�����ɵ� c-model ����--c_model_name Ĭ����network
python aitools.py --project=<your_project_path> --model=<your_model_path> --platform=stm32 --ext_tools=<your_x-cube-ai_path> --c_model_name=<new_model_name>
```

��������Ŀʵս���̣����Ķ���[RT-AK֮STM32��������.md](./docs/RT-AK֮STM32��������.md)

## �����б�

- [x] �ж�ģ���Ƿ�֧��
- [x] �ж� `CPU` �Ƿ�֧��
- [x] ���� `stm32ai` ϵͳ����������`x-cube-ai`
- [x] �� `stm_out` �����ɾ�̬���ļ��кʹ�� `c-model` ���ļ���
- [x] ��ģ��ת���� `c-model`�������� `<stm_out>/X-CUBE-AI` ·����
- [x] ���� `rt_ai_<model_name>_model.h` �ļ��������� `project/applications` 
- [x] ���� `rt_ai_<model_name>_model.c` �ļ��������� `project/applications` 
- [x] ���� `x-cube-ai` �ľ�̬�⵽ `stm_out` ·����
- [x] �� `stm_out` �ڵ������ؼ��ļ��м��ص� `project` ��
- [x] �� `project` ��ʹ�� `HAL_CRC`
- [x] �ж��Ƿ�ɾ�� `stm_out`

<details>
<summary>���ܺ���</summary> 
<pre><code>
1 ģ���Ƿ�֧��
- ������`is_valid_model(model, sup_models)`
- ���ܣ��ж�ģ���Ƿ�֧��
- input: (model, sup_models_list)
<br>
2 cpu�Ƿ�֧��
- ������`is_valid_cpu(project, sup_cpus, cpu="")`
- ���ܣ����� `project/rtconfig.py` �ṩ�� `CPU` ��Ϣ�ж��Ƿ�֧��
- input: (project, sup_cpus)
- output: cpu
<br>
3 ���û�������
- ������`set_env(plugin_path)`
- ���ܣ����� `x-cube-ai: stm32.exe` Ϊϵͳ����
- input: (x-cube-ai_path)
<br>
4 ���������ļ���
- ������`pre_sconscript(aitools_out, stm32_dirs, scons_path="platforms/stm32/Sconscripts")`
- ���ܣ�
  1. ���������ļ��У��ֱ��� `x-cube-ai` ��̬��� `c-model` �ļ������֮ǰ���ڣ���ɾ��ԭ�����ļ���
  2. ���ض�Ӧ�� `Sconscript`
- input: (stm_out, sconscript_dir, ["Middlewares", "X-CUBE-AI"])
<br>
5 ģ��ת��
- ������`stm32ai(model, stm_out, c_model_name, sup_modes, ai_params)`
- ���ܣ�
  1. ��ģ��ת���� `c-model`��֧������ģʽ����������֤�����ɣ������У�
  2. ����б����������ɵ� `report.txt` �ļ��׳��쳣
- input: (model, stm_out, c_model_name, sup_modes_list, [workspace, compress, batches, mode, val_data])
- output: flag_list, etc: [False, True, True] ��Ӧ modes=��011�� ����ģ��ִ���Ƿ�ɹ�
<br>
6.1 ���� rt_ai_model.h
- ������`rt_ai_model_gen(stm_out, project, model_name)`
- ���ܣ��������ɵ� `c-model` �ļ�����  `rt_ai_<model_name>_model.h` �ļ��������� `project/applications` 
- input: (stm_out, project, c_model_name)
<br>
6.2 ���� rt_ai_model.c
- ������`load_rt_ai_example(project, rt_ai_example, platform, old_name, new_name)`
- ���ܣ������ṩ��ģ���ļ������� `rt_ai_<model_name>_model.c` + `rt_ai_template.c/h`�ļ��������� `project/applications` 
- input: (project, rt_ai_exampl_path, platform, default_model_name, c_model_name)
<br>
7 ���� x-cube-ai libs
- ������`load_lib(stm_out, cube_ai_path, cpu, middle=r"Middlewares/ST/AI")`
- ���ܣ����� `x-cube-ai` ��̬�⵽ `stm_out` ��
- input: (stm_out, cube_ai_path, cpu, middle=r"Middlewares/ST/AI")
<br>
8 ���ص� project
- ������`load_to_project(stm_out, project, stm32_dirs)`
- ���ܣ����� `stm_out` �����ļ��е� `project` �С����֮ǰ�д��ڣ�����ɾ��
- input: (stm_out, project, ["Middlewares", "X-CUBE-AI"])
<br>
9 ʹ�� HAL-CRC
- ������`enable_hal_crc(project)`
- ���ܣ��� `project/board/...` �ļ���ʹ�� `HAL_CRC_MODULE_ENABLED`
- input: (project)
</code></pre>
</details>