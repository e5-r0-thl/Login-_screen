## الاسم: مرام وديع
## التخصص: تقنية معلومات
## اسم المشروع: مستكشف الفضاء

## شرح التكليف
التكليف عبارة عن بناء تطبيق تسجيل الدخول  باستخدام إطار عمل Flutter.
## تقرير واجهة فورم تسجيل الدخول (Space Login)
## أولاً: هيكلة التصميم (Layout)
​تم استخدام عدة عناصر برمجية لتنظيم محتوى الشاشة وضمان تناسقها:
​ويدجت Stack: تم استخدامه كحاوية أساسية للشاشة لوضع "صورة الخلفية" في الطبقة الأولى، ومن ثم بناء "واجهة الإدخال" في الطبقة الثانية فوقها.
​ويدجت Center: استُخدم لضمان بقاء صندوق تسجيل الدخول في منتصف الشاشة تماماً بغض النظر عن حجم الجهاز.
​ويدجت Container مع BoxConstraints: تم تحديد عرض أقصى (350px) للصندوق لضمان أن الفورم لا يتمدد بشكل غير مريح على الشاشات العريضة، مما يحافظ على مظهر احترافي ومنظم.
​ويدجت SingleChildScrollView: لضمان قابلية التمرير في حال كانت الشاشة صغيرة أو عند ظهور لوحة المفاتيح، لمنع حدوث أخطاء تجاوز المساحة (Overflow).
## ثانياً: التنسيق الجمالي (Styling)
​تم اختيار الستايل ليعكس طابعاً تقنياً (Futuristic) باستخدام الخصائص التالية:
​الشفافية (Opacity): استُخدم اللون الأسود بطلية شفافة (0.8) للخلفية؛ وذلك للسماح برؤية جزء من النجوم في الخلفية مع الحفاظ على وضوح نصوص الإدخال.
​الحواف الدائرية
 (BorderRadius): تم تطبيق انحناء بمقدار (25) للحواف لإضفاء لمسة عصرية وناعمة على الواجهة.
​الحدود المتوهجة
 (Border): تم استخدام اللون (CyanAccent) ليكون هو اللون الأساسي للحدود، مما يعطي إيحاءً بالأنظمة الإلكترونية المتقدمة.
​الظلال المضيئة (BoxShadow): تم إضافة ظل بلون الـ Cyan مع خاصية blurRadius لخلق تأثير التوهج (Glow Effect) حول صندوق الدخول.
## ثالثاً: عناصر الإدخال والأزرار
​تنسيق الـ TextField:
​تم استخدام OutlineInputBorder لتحديد شكل الحقول.
​تم تخصيص الألوان لتكون متناسقة مع الثيم العام (نصوص بيضاء وحدود سماوية).
​استخدام prefixIcon داخل الحقول لتسهيل التعرف البصري على وظيفة كل حقل (أيقونة الشخص للاسم، والمفتاح للرمز).
​تنسيق الزر (ElevatedButton):
​تم اختيار لون خلفية بارز (CyanAccent) مع نص أسود لخلق تباين عالي (High Contrast) يسهل على المستخدم رؤية زر التنفيذ الأساسي فوراً.
​تم جعل الزر يأخذ العرض الكامل للحاوية لسهولة الضغط عليه
## رابعاً: التفاعل المباشر (Feedback)
​رسالة التنبيه (SnackBar): تم استخدامها لتأكيد نجاح العملية برمجياً فور الضغط على الزر، مما يعطي انطباعاً فورياً للمستخدم بأن النظام استجاب لطلبه بنجاح قبل الانتقال لأي مرحلة أخرى.
## الكود الكامل
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(
    const MaterialApp(
      debugShowCheckedModeBanner: false,
      home: SpaceLoginScreen(),
    ),
  );
}

class SpaceLoginScreen extends StatelessWidget {
  const SpaceLoginScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Stack(
        children: [
          Container(
            width: double.infinity,
            height: double.infinity,
            decoration: const BoxDecoration(
              image: DecorationImage(
                image: NetworkImage(
                  'https://images.unsplash.com/photo-1451187580459-43490279c0fa?q=80&w=1000',
                ),
                fit: BoxFit.cover,
              ),
            ),
          ),
          Center(
            child: SingleChildScrollView(
              child: Container(
                constraints: const BoxConstraints(maxWidth: 350),
                margin: const EdgeInsets.symmetric(horizontal: 20),
                padding: const EdgeInsets.all(30),
                decoration: BoxDecoration(
                  color: Colors.black.withOpacity(0.8), // شفافية سوداء
                  borderRadius: BorderRadius.circular(25),
                  border: Border.all(color: Colors.cyanAccent, width: 1.5),
                  boxShadow: [
                    BoxShadow(
                      color: Colors.cyanAccent.withOpacity(0.3),
                      blurRadius: 15,
                      spreadRadius: 2,
                    ),
                  ],
                ),
                child: Column(
                  mainAxisSize: MainAxisSize.min,
                  children: [
                    const Icon(
                      Icons.rocket_launch,
                      size: 60,
                      color: Colors.cyanAccent,
                    ),
                    const SizedBox(height: 15),
                    const Text(
                      style: TextStyle(
                        color: Colors.white,
                        fontSize: 24,
                        fontWeight: FontWeight.bold,
                        letterSpacing: 1.2,
                      ),
                    ),
                    const SizedBox(height: 30),

                    TextField(
                      style: const TextStyle(color: Colors.white),
                      decoration: InputDecoration(
                        labelText: "اسم المكتشف",
                        labelStyle: const TextStyle(color: Colors.cyanAccent),
                        prefixIcon: const Icon(
                          Icons.person,
                          color: Colors.cyanAccent,
                        ),
                        enabledBorder: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(30),
                          borderSide: const BorderSide(
                            color: Colors.cyanAccent,
                          ),
                        ),
                        focusedBorder: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(30),
                          borderSide: const BorderSide(color: Colors.white),
                        ),
                      ),
                    ),

                    const SizedBox(height: 15),

                    TextField(
                      obscureText: true,
                      style: const TextStyle(color: Colors.white),
                      decoration: InputDecoration(
                        labelText: "رمز الدخول",
                        labelStyle: const TextStyle(color: Colors.cyanAccent),
                        prefixIcon: const Icon(
                          Icons.vpn_key,
                          color: Colors.cyanAccent,
                        ),
                        enabledBorder: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(30),
                          borderSide: const BorderSide(
                            color: Colors.cyanAccent,
                          ),
                        ),
                        focusedBorder: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(30),
                          borderSide: const BorderSide(color: Colors.white),
                        ),
                      ),
                    ),

                    const SizedBox(height: 30),

                    ElevatedButton(
                      style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.cyanAccent,
                        foregroundColor: Colors.black,
                        minimumSize: const Size(double.infinity, 50),
                        shape: RoundedRectangleBorder(
                          borderRadius: BorderRadius.circular(30),
                        ),
                      ),
                      onPressed: () {
                        ScaffoldMessenger.of(context).showSnackBar(
                          const SnackBar(
                            content: Text("تم تسجيل الدخول بنجاح!"),
                            backgroundColor: Colors.green,
                            behavior: SnackBarBehavior.floating,
                          ),
                        );

                        Navigator.push(
                          context,
                          MaterialPageRoute(
                            builder: (context) => const WelcomeSpaceScreen(),
                          ),
                        );
                      },
                      child: const Text(
                        style: TextStyle(fontWeight: FontWeight.bold),
                      ),
                    ),
                  ],
                ),
              ),
            ),
          ),
        ],
      ),
    );
  }
}

class WelcomeSpaceScreen extends StatelessWidget {
  const WelcomeSpaceScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.black,
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            const Icon(Icons.stars, color: Colors.yellow, size: 100),
            const SizedBox(height: 20),
            const Text(
              "أهلاً بك في المحطة الفضائية",
              style: TextStyle(
                color: Colors.white,
                fontSize: 20,
                fontWeight: FontWeight.bold,
              ),
            ),
            const SizedBox(height: 40),
            ElevatedButton.icon(
              onPressed: () => Navigator.pop(context),
              icon: const Icon(Icons.arrow_back),
              label: const Text("رجوع "),
              style: ElevatedButton.styleFrom(
                backgroundColor: Colors.redAccent,
                foregroundColor: Colors.white,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```
## لقطة شاشة تسجيل الدخول
![Masar Platform Login](https://i.postimg.cc/7J6s8QXZ/loginscreen.png)

