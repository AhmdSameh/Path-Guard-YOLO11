# Path-Guard-YOLO11
Path Guard - AI-Powered Obstacle Detection for the Visually Impaired Path Guard is a cutting-edge Computer Vision solution designed to enhance the mobility and safety of visually impaired individuals. The system functions as a "digital eye," detecting and classifying street obstacles in real-time.

(ركز على اخر مقطع لمعرفة كيفية تشغيل الكود)

Technical Highlights:
Core Architecture: Built using YOLO11m.pt, providing a robust balance between inference speed and detection precision.
Performance: Achieved an overall 85% Accuracy (mAP50), significantly outperforming lighter models in detecting complex hazards like potholes and road cracks.
Comprehensive Detection: Capable of identifying 9 critical classes: (Cars, Motorcycles, Vans, Potholes, Cracked Tiles, Roads, Sidewalks, Steps, and Walls).
User-Centric Design: Includes a flexible module for uploading personal media (images/videos) for instant AI analysis.
Real-Time Visualization: Optimized with a JavaScript-Python bridge for smooth, low-latency video streaming and live bounding box rendering.

                                                                                                                                                                
يعتبر مشروع Path Guard حلاً تقنياً متطوراً يعتمد على الرؤية الحاسوبية (Computer Vision)، صُمم خصيصاً لتعزيز القدرة على الحركة والأمان للأفراد ذوي الإعاقة البصرية. يعمل النظام بمثابة "عين رقمية" تقوم برصد وتصنيف عوائق الطريق في الوقت الفعلي.

أبرز النقاط التقنية:
البنية التحتية للنظام: تم بناء المشروع باستخدام نموذج YOLO11m.pt، مما يوفر توازناً قوياً بين سرعة الاستجابة ودقة الكشف.
الأداء: حقق النظام دقة إجمالية وصلت إلى 85% (mAP50)، متفوقاً بشكل ملحوظ على النماذج الأخف في كشف المخاطر المعقدة مثل الحفر وتشققات الطريق.
كشف شامل للعوائق: يتمتع النظام بالقدرة على تحديد 9 فئات حيوية وهي: (السيارات، الدراجات النارية، الشاحنات، الحفر، تشققات البلاط، الطرق، الأرصفة، السلالم، والجدران).
تصميم يركز على المستخدم: يتضمن النظام وحدة مرنة تسمح برفع الوسائط الشخصية (صور/فيديوهات) لإجراء تحليل فوري بواسطة الذكاء الاصطناعي.
عرض بصري في الوقت الفعلي: تم تحسين النظام باستخدام "جسر" برمي بين لغتي JavaScript وPython لضمان تدفق فيديو سلس ومنخفض التأخير، مع إظهار مربعات التحديد (Bounding Boxes) الحية بشكل انسيابي.

 The Path Guard Journey: From Raw Data to Real-Time Inference
 
1. Data Collection & Preparation (Label Studio Stage):
The Beginning: We acquired a large-scale dataset (approx. 18,000 images) in COCO format from Roboflow and Kaggle.
Defining Obstacles: We focused on 9 critical classes for the visually impaired (Cars, Motorcycles, Vans, Potholes, Cracked Tiles, Roads, Sidewalks, Steps, and Walls).
Using Label Studio: This professional tool was used for Image Annotation. We manually drew precise bounding boxes around obstacles to teach the model how to recognize location and type.

2. Training Phase:
We trained the YOLO11m (Medium) model to achieve an accuracy of 85%. This version was selected over lighter ones for its superior ability to detect complex hazards like road cracks.

3. Code Workflow Overview
Environment Setup: The code initializes by installing necessary libraries like ultralytics for YOLO and OpenCV for image/video processing, while clearing old directories to ensure a clean workspace.
training: It changes the images sizes to 480*480 to make it faster then It uses GPU T4 to learn the bounding boxes that was drawn around obstacles in them. 
File Management: It automatically extracts my_model.zip to locate the trained weights (best.pt). This ensures the system is operational as soon as the client provides the validation file.
Data Preparation: The script handles the extraction of validation.zip containing test images or test_video.mp4 (given by client). Files are organized into specific directories for the AI engine to access.
Inference Engine: This is the core of the project where the YOLO11m model (85% accuracy) is loaded. It scans images or video frames, identifies obstacle locations, and classifies them based on the knowledge gained during the labeling stage (Label Studio) and training phase.
Image Visualization Module: Post-inference, the code retrieves the latest results and displays images sequentially. Key highlights include rendering colorful bounding boxes and labels directly on detected objects for easy evaluation.
Real-Time Video Stream Module: For video processing, the code implements a "bridge" between Python processing and JavaScript rendering. By resizing frames and enabling FP16 precision (half=True), it achieves a high-speed, smooth visual experience that mimics real-world application.

Code Walkthrough (The Final Two Modules):
These scripts are tailored for the client to run the system seamlessly using my_model.zip (containing best.pt) and their specific data files.

A- Image Prediction & Visualization Code:
Purpose: Allows the client to upload a file named validation.zip containing any images they wish to test.

Mechanism:
Extracts the model to access the best.pt weight file.
Extracts the client's images into a validation_data folder.
Executes the YOLO predict command on the source folder.
Visualization Feature: Uses IPython.display to fetch the latest detection results and display the images sequentially, showing clear colored bounding boxes and labels for each obstacle.

B- Turbo Real-Time Video Mode:
Purpose: Designed for dynamic footage (whith the name: test_video.mp4), optimized for high performance on powerful GPUs.

Mechanism:
Processes the video frame-by-frame using an Inference Stream.
Turbo Optimization: We implemented frame resizing and enabled half=True (FP16 inference) to double the processing speed on the GPU.

JavaScript Bridge: Instead of flickering images, we embedded a JavaScript snippet within Python to update a static display container. This provides the client with a smooth, actual video experience where obstacles are tracked in real-time. 

رحلة Path Guard: من البيانات الخام إلى الاستدلال اللحظي
1. جمع البيانات وتحضيرها (مرحلة Label Studio):
البداية: حصلنا على مجموعة بيانات ضخمة (حوالي 18,000 صورة) بتنسيق COCO من منصتي Roboflow وKaggle.
تحديد العقبات: ركزنا على 9 فئات أساسية تشكل خطورة على الكفيف: (السيارات، الدراجات النارية، الشاحنات، الحفر، تشققات البلاط، الطرق، الأرصفة، السلالم، والجدران).
استخدام Label Studio: تم استخدام هذه الأداة الاحترافية لتحديد العقبات فى الصور؛ حيث قمنا برسم مربعات تحديد دقيقة حول العقبات لتعليم النموذج كيفية التعرف على الموقع والنوع.

2. مرحلة التدريب:
قمنا بتدريب نموذج YOLO11m (النسخة المتوسطة) للوصول إلى دقة 85%. تم اختيار هذا الإصدار بدلاً من النسخ الأخف نظراً لقدرته الفائقة على اكتشاف المخاطر المعقدة مثل تشققات الطريق.

3. نظرة عامة على سير عمل الكود:
إعداد البيئة: يبدأ الكود بتثبيت المكتبات الضرورية مثل ultralytics و OpenCV مع تنظيف المجلدات القديمة لضمان بيئة عمل منظمة.
التدريب: يتم تغيير حجم الصور إلى (480x480) لزيادة السرعة، مع استخدام المعالج الرسومي GPU T4 لتعلم المربعات المحيطة بالعقبات.
إدارة الملفات: يقوم النظام تلقائياً بفك ضغط ملف my_model.zip لتحديد موقع أوزان الموديل (best.pt)؛ مما يضمن جاهزية النظام فور توفير ملفات الاختبار.
تحضير البيانات: يعالج الكود فك ضغط ملف validation.zip (الصور) أو فيديو test_video.mp4 المقدم من العميل، وينظمها في مجلدات خاصة لمحرك الذكاء الاصطناعي.
محرك الاستدلال: هذا هو قلب المشروع؛ حيث يتم تحميل موديل YOLO11m بدقة 85% لمسح الصور أو إطارات الفيديو وتصنيف العقبات بناءً على ما تعلمه في مرحلتي الوسم والتدريب.
وحدة عرض الصور: بعد انتهاء التحليل، يسترجع الكود أحدث النتائج ويعرض الصور بشكل متسلسل مع رسم مربعات التحديد الملونة والتسميات لسهولة التقييم.
وحدة بث الفيديو اللحظي: بالنسبة للفيديو، يطبق الكود "جسر" برمجياً يربط بين معالجة Python وعرض JavaScript. عبر تغيير حجم الإطارات وتفعيل دقة FP16 (half=True)؛ يحقق النظام تجربة بصرية سلسة وعالية السرعة تحاكي التطبيق في الواقع.

شرح تفصيلي للأكواد (آخر وحدتين برمجيتين):
هذه الأكواد مخصصة للعميل لتشغيل النظام بسلاسة باستخدام موديله الخاص وبياناته الشخصية.

أ- كود التنبؤ وعرض الصور:
الهدف: يتيح للعميل رفع ملف validation.zip يحتوي على أي صور يريد اختبارها.

آلية العمل:
فك ضغط الموديل للوصول إلى ملف best.pt.
استخراج صور العميل إلى مجلد validation_data.
تنفيذ أمر التنبؤ على المجلد المصدر.
ميزة العرض: يستخدم مكتبة IPython.display لجلب أحدث النتائج وعرضها متسلسلة بمربعات تحديد واضحة لكل عائق.

ب- وضع الفيديو السريع:
الهدف: مصمم للمقاطع الحركية (باسم test_video.mp4) ومحسن للأداء العالي على المعالجات الرسومية القوية.

آلية العمل:
يعالج الفيديو إطاراً تلو الآخر عبر تدفق الاستدلال.
تحسين "التوربو": تم تطبيق تغيير حجم الإطارات وتفعيل وضع half=True لمضاعفة سرعة المعالجة على الـ GPU.

جسر JavaScript: بدلاً من الصور المتقطعة، قمنا بدمج كود JavaScript داخل Python لتحديث حاوية عرض ثابتة؛ مما يمنح العميل تجربة فيديو حقيقية وسلسة يتم فيها تتبع العقبات في الوقت الفعلي.




 لتشغيل الكود إليك ست جمل مختصرة توضح الخطوات المطلوبة لتشغيل النظام بنجاح:

1- اذا لم ترد اعداد بيانات(صور + علامات) التى تحتاجها للتدريب كما وضحت فوق- قم برفع ملف الموديل المدرب باسم my_model.zip الذي يحتوي على أوزان الموديل (best.pt) إلى مجلد الملفات الرئيسي(Files) فى كولاب فى الملف Path Guard.ipynb و تأكد من استخدام GPU T4 كruntime type.

2-ارفع الصور التي ترغب في فحصها داخل ملف مضغوط باسم validation.zip إلى مجلد الملفات الرئيسي(Files) فى كولاب ليتعرف عليها النظام تلقائياً.

3-إذا كنت ترغب في تحليل مقطع فيديو، قم برفع الفيديو وتأكد من تسميته test_video.mp4 إلى مجلد الملفات الرئيسي(Files) ايضا لضمان تشغيل وضع "التوربو" السريع .

4-قم بتشغيل اخر خليتين فى الملف Path Guard.ipynb
أ-خلية "كود الصور" لعرض النتائج بشكل متسلسل مع المربعات التعريفية لكل عائق تم اكتشافه.

ب-خلية "كود الفيديو" لمشاهدة تحليل مباشر وانسيابي يوضح كيفية تتبع النظام للعوائق في الوقت الفعلي.
