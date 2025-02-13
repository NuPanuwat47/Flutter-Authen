# Flutter-Authen
 
1. ฟังก์ชัน _login() --> Login_screen.dart
-รับข้อมูลจาก _emailController และ _passwordController
-ตรวจสอบว่า email และ password ไม่ว่าง
-ใช้ FirebaseAuth เพื่อล็อกอินด้วย signInWithEmailAndPassword()
-หากสำเร็จจะเปลี่ยนหน้า

2. ฟังก์ชัน _showForgotPasswordDialog() --> Login_screen.dart
-สร้างหน้าต่างป๊อปอัปด้วย showDialog สำหรับให้กรอก email
-TextField: ให้ผู้ใช้ป้อนอีเมลเพื่อขอรีเซ็ตรหัสผ่าน
-ปุ่ม Cancel: ปิดหน้าต่าง
-ปุ่ม Submit: เรียก _forgotPassword() พร้อมส่ง email ที่กรอกไป

3. ฟังก์ชัน _forgotPassword() --> Login_screen.dart
-ตรวจสอบอีเมล: ถ้าว่างจะแจ้งเตือนให้กรอก
-ส่งคำขอรีเซ็ตรหัสผ่าน: ใช้ FirebaseAuth ผ่าน sendPasswordResetEmail()
-แจ้งเตือนความสำเร็จ: แสดง SnackBar ว่าส่งอีเมลสำเร็จแล้ว
-จัดการข้อผิดพลาด: แสดงข้อความ Error หากล้มเหลว

4. ฟังก์ชัน _logout() --> home_screen.dart
-เรียกออกจากระบบ: ใช้ FirebaseAuth.instance.signOut() เพื่อลบ session การเข้าสู่ระบบปัจจุบัน
-เปลี่ยนหน้า: หลังจากออกจากระบบ จะเปลี่ยนกลับไปที่ LoginScreen ด้วย Navigator.pushReplacement()
-จัดการข้อผิดพลาด: หากเกิดปัญหา จะใช้ SnackBar แจ้งข้อความ Logout failed: $e

5. ฟังก์ชัน build() --> home_screen.dart
   สร้าง UI หลัก:
      AppBar:
          แสดงชื่อว่า "Home Screen"
          มีปุ่ม Logout (รูปไอคอน 🔓) ซึ่งเมื่อกดจะเรียก _logout()
      Body:
          แสดงข้อความกลางหน้าว่า "Welcome to the Home Screen!"

6. ฟังก์ชัน _createAccount --> create_account_screen.dart
-อ่านข้อมูลจาก TextField → email, password, confirmPassword
-ตรวจสอบความถูกต้อง:
      ช่องว่าง → แจ้ง Please fill all fields
      รหัสผ่านไม่ตรงกัน → แจ้ง Passwords do not match
-สร้างบัญชีด้วย Firebase:
      สำเร็จ: แจ้ง Account created และ Navigator.pop เพื่อกลับไปหน้า Login
      ล้มเหลว: แสดงข้อความผิดพลาด เช่น
            weak-password → The password provided is too weak.
            email-already-in-use → The account already exists for that email.
            อื่น ๆ: แสดงข้อความ Error: $e

7. ฟังก์ชัน LoginScreen() --> main.dart
-แสดงหน้า Login
