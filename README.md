# HomeGrid-EaaS — الطاقة المنزلية كخدمة (تصميم نظري)

> **حالة المشروع:** تصميم نظري ووثائق فقط. لا يوجد كود تنفيذي ولا مخططات تصنيع.
> **تنبيه:** كل الأرقام (الأسعار، التكاليف، الحسابات) تقديرية لأغراض الدراسة، ويجب التحقق منها ميدانياً قبل أي تنفيذ. الأنظمة الكهربائية عالية القدرة والبطاريات خطرة وتتطلب فنيين مؤهلين ومطابقة للأنظمة المحلية.

## الفكرة

منظومة طاقة منزلية (بطارية ليثيوم وإنفيرتر) **تملكها الشركة وتؤجرها باشتراك شهري** بدلاً من مولدة الحي. تتصل المنظومة بالإنترنت، ويتحكم بها خادم مركزي في التفعيل والقطع وحدود الاستهلاك، مع مراقبة مضادة للسرقة.

**السياق:** العراق، حيث توزع مولدات الأحياء الكهرباء بالأمبير (6 إلى 10 A للمنزل النموذجي) وتكثر الأعطال وعدم استقرار الفولتية.

## لماذا بديل جيد عن المولدة

| الميزة | التفصيل |
|---|---|
| انقطاع صفري تقريباً | الإنفيرتر يعمل بوضع UPS فيتحول فورياً بين الوطنية والبطارية |
| استقرار الفولتية | جهد خرج منتظم من الإنفيرتر |
| بلا أسلاك حي | لا تمديدات مشتركة ولا أعطال ناتجة عنها |
| سداد وتحكم سهلان | دفع إلكتروني، وتفعيل تلقائي، وتجميد الاشتراك للمسافر |
| لا وقود ولا ضجيج | |

## المنظومة بنظرة سريعة

| المكوّن | القيمة المرجعية |
|---|---|
| البطارية | LiFePO4، 15 kWh، مع BMS يدعم CAN |
| الإنفيرتر | هجين 5 kW، يدعم RS485/Modbus |
| المصدر | الشبكة الوطنية (والألواح اختيارية للباقات المميزة) |
| المتحكم | ESP32 مع عداد AC وكونتاكتور على خرج الإنفيرتر |
| الاتصال | WiFi (المرحلة الأولى)، مع خيار 4G لاحقاً |
| السحابة | MQTT على TLS، وخادم تطبيقات وقاعدة بيانات |

## الباقات (مرجعية)

| الباقة | الحد | سعر الصيف (8 أشهر) | سعر الشتاء (4 أشهر) |
|---|---|---|---|
| 6 A | 1.3 kW | 90,000 د.ع | 48,000 د.ع |
| 8 A | 1.8 kW | 120,000 د.ع | 64,000 د.ع |
| 10 A | 2.2 kW | 150,000 د.ع | 80,000 د.ع |

الأسعار بنفس سعر الأمبير لدى المولدة (15,000 صيفاً و8,000 شتاءً). التفاصيل في [النموذج المالي](docs/07-financial-model.md).

## فهرس الوثائق

| الملف | المحتوى |
|---|---|
| [01-requirements.md](docs/01-requirements.md) | المتطلبات الوظيفية وغير الوظيفية وقواعد الأعمال |
| [02-architecture.md](docs/02-architecture.md) | المعمارية العامة وقرارات التصميم |
| [03-hardware-design.md](docs/03-hardware-design.md) | تصميم العتاد وحسابات الأبعاد |
| [04-control-and-firmware.md](docs/04-control-and-firmware.md) | منطق التحكم، وحدّ التيار، وكشف السرقة، ورمز الصلاحية |
| [05-cloud-and-api.md](docs/05-cloud-and-api.md) | السحابة، وبروتوكول MQTT، ونموذج البيانات، وواجهات API |
| [06-security-and-safety.md](docs/06-security-and-safety.md) | نموذج التهديدات وإجراءات الأمان والسلامة |
| [07-financial-model.md](docs/07-financial-model.md) | الجدوى والاسترداد والحساسية |
| [08-roadmap.md](docs/08-roadmap.md) | المراحل والتجربة الأولية والمخاطر |

## English summary

**HomeGrid-EaaS** is a *theoretical design* for a subscription-based home energy service in Iraq, intended to replace neighborhood diesel generators. Each home gets a company-owned unit (15 kWh LiFePO4 battery + 5 kW hybrid inverter) charged from the national grid, with an ESP32-based controller that enforces the subscription (amp limit, expiry cut-off, freeze), detects battery power theft (BMS vs. inverter current mismatch, energy balance, tamper switch), and reports to a cloud dashboard (green/orange/red/grey status per subscriber). The repository contains requirements, architecture, hardware sizing, control logic, cloud/API design, security, financial model and roadmap. No implementation code is included. All figures are rough estimates.

## الترخيص

لم يُحدَّد بعد. يُنصح باختيار ترخيص (مثل CC BY 4.0 للوثائق) قبل النشر.
