# Flutter-Authen <br>

1. ฟังก์ชัน _login() --> Login_screen.dart <br>
-รับข้อมูลจาก _emailController และ _passwordController <br>
-ตรวจสอบว่า email และ password ไม่ว่าง <br>
-ใช้ FirebaseAuth เพื่อล็อกอินด้วย signInWithEmailAndPassword() <br>
-หากสำเร็จจะเปลี่ยนหน้า <br>
2. ฟังก์ชัน _showForgotPasswordDialog() --> Login_screen.dart <br>
-สร้างหน้าต่างป๊อปอัปด้วย showDialog สำหรับให้กรอก email <br>
-TextField: ให้ผู้ใช้ป้อนอีเมลเพื่อขอรีเซ็ตรหัสผ่าน <br>
-ปุ่ม Cancel: ปิดหน้าต่าง <br>
-ปุ่ม Submit: เรียก _forgotPassword() พร้อมส่ง email ที่กรอกไป <br>
3. ฟังก์ชัน _forgotPassword() --> Login_screen.dart <br>
-ตรวจสอบอีเมล: ถ้าว่างจะแจ้งเตือนให้กรอก <br>
-ส่งคำขอรีเซ็ตรหัสผ่าน: ใช้ FirebaseAuth ผ่าน sendPasswordResetEmail() <br>
-แจ้งเตือนความสำเร็จ: แสดง SnackBar ว่าส่งอีเมลสำเร็จแล้ว <br>
-จัดการข้อผิดพลาด: แสดงข้อความ Error หากล้มเหลว <br>
4. ฟังก์ชัน _logout() --> home_screen.dart <br>
-เรียกออกจากระบบ: ใช้ FirebaseAuth.instance.signOut() เพื่อลบ session การเข้าสู่ระบบปัจจุบัน <br>
-เปลี่ยนหน้า: หลังจากออกจากระบบ จะเปลี่ยนกลับไปที่ LoginScreen ด้วย Navigator.pushReplacement() <br>
-จัดการข้อผิดพลาด: หากเกิดปัญหา จะใช้ SnackBar แจ้งข้อความ Logout failed: $e <br>
5. ฟังก์ชัน build() --> home_screen.dart <br>
   สร้าง UI หลัก: <br>
      AppBar: <br>
          แสดงชื่อว่า "Home Screen" <br>
          มีปุ่ม Logout (รูปไอคอน 🔓) ซึ่งเมื่อกดจะเรียก _logout() <br>
      Body: <br>
          แสดงข้อความกลางหน้าว่า "Welcome to the Home Screen!" <br>
6. ฟังก์ชัน _createAccount --> create_account_screen.dart <br>
-อ่านข้อมูลจาก TextField → email, password, confirmPassword <br>
-ตรวจสอบความถูกต้อง: <br>
      ช่องว่าง → แจ้ง Please fill all fields <br>
      รหัสผ่านไม่ตรงกัน → แจ้ง Passwords do not match <br>
-สร้างบัญชีด้วย Firebase: <br>
      สำเร็จ: แจ้ง Account created และ Navigator.pop เพื่อกลับไปหน้า Login <br>
      ล้มเหลว: แสดงข้อความผิดพลาด เช่น <br>
            weak-password → The password provided is too weak. <br>
            email-already-in-use → The account already exists for that email. <br>
            อื่น ๆ: แสดงข้อความ Error: $e <br>
7. ฟังก์ชัน LoginScreen() --> main.dart <br>
-แสดงหน้า Login <br>
