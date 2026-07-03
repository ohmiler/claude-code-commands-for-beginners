# คำสั่ง Claude Code ที่ใช้บ่อย สำหรับมือใหม่

## ไม่ต้องจำทุกคำสั่ง แค่รู้ชุดนี้ก็ใช้งาน Claude Code คล่องขึ้นเยอะ

เวลามือใหม่เริ่มใช้ Claude Code สิ่งที่มักทำให้งงคือ “คำสั่งเยอะมาก ไม่รู้ต้องใช้ตัวไหนก่อน”

จริง ๆ แล้ว Claude Code มีคำสั่งหลัก ๆ อยู่ 2 แบบ

1. **CLI Commands** คือคำสั่งที่พิมพ์ใน Terminal เช่น `claude`, `claude -p`, `claude -c`
2. **Slash Commands** คือคำสั่งที่พิมพ์ตอนอยู่ใน session ของ Claude Code เช่น `/init`, `/plan`, `/compact`, `/diff`

ในเอกสารทางการ Claude Code ระบุว่า slash command ใช้ควบคุม Claude Code จากใน session และสามารถพิมพ์ `/` เพื่อดูคำสั่งทั้งหมดหรือกรองคำสั่งที่ต้องการได้ โดยคำสั่งต้องขึ้นต้นข้อความถึงจะทำงานเป็น command

---

## 1. คำสั่งกลุ่ม CLI ที่ใช้ใน Terminal

คำสั่งกลุ่มนี้ใช้ตอนเราอยู่ใน Terminal ก่อนหรือระหว่างเริ่มใช้งาน Claude Code โดยเอกสาร CLI reference ระบุว่าสามารถใช้เพื่อเริ่ม session, ส่ง prompt แบบครั้งเดียว, pipe ข้อมูล, resume งานเดิม และจัดการ account/update ได้

| คำสั่ง                                | ความหมาย                                     | ใช้ตอนไหน                             |
| ------------------------------------- | -------------------------------------------- | ------------------------------------- |
| `claude`                              | เปิด Claude Code แบบ interactive             | ใช้เริ่มทำงานในโปรเจกต์               |
| `claude "explain this project"`       | เปิด Claude พร้อม prompt แรก                 | ใช้ให้ Claude วิเคราะห์โปรเจกต์ทันที  |
| `claude -p "explain this function"`   | ส่งคำถามแบบครั้งเดียว แล้วจบการทำงาน         | เหมาะกับงานสั้น ๆ หรือใช้ใน script    |
| `cat logs.txt \| claude -p "explain"` | ส่งเนื้อหาไฟล์เข้า Claude ผ่าน pipe          | เหมาะกับการวิเคราะห์ log/error        |
| `claude -c`                           | ต่อ conversation ล่าสุดใน directory ปัจจุบัน | ใช้กลับมาทำงานเดิมต่อ                 |
| `claude -r "<session>" "query"`       | resume session ด้วยชื่อหรือ ID               | ใช้กลับไปคุยงานเดิมแบบเฉพาะเจาะจง     |
| `claude update`                       | อัปเดต Claude Code                           | ใช้ให้เครื่องมี version ล่าสุด        |
| `claude auth login`                   | login เข้า account                           | ใช้ตอนเริ่มตั้งค่า                    |
| `claude auth logout`                  | logout ออกจาก account                        | ใช้ตอนเปลี่ยน account                 |
| `claude auth status`                  | เช็กสถานะ login                              | ใช้ตอนสงสัยว่า account พร้อมใช้งานไหม |

ตัวอย่างที่มือใหม่ใช้บ่อย:

```bash
claude
```

ใช้เปิด Claude Code ในโปรเจกต์ปัจจุบัน

```bash
claude -p "สรุปโครงสร้างโปรเจกต์นี้ให้หน่อย"
```

ใช้ถามแบบเร็ว ๆ โดยไม่ต้องเข้า session ยาว

```bash
cat error.log | claude -p "ช่วยวิเคราะห์ error นี้ให้หน่อย"
```

ใช้โยน log ให้ Claude วิเคราะห์

---

## 2. คำสั่ง Slash Commands ที่ใช้ใน Claude Code Session

เวลาคุณเปิด `claude` เข้าไปแล้ว คำสั่งที่ขึ้นต้นด้วย `/` จะช่วยควบคุมการทำงาน เช่น วางแผน, เคลียร์ context, ดู diff, ตรวจ code review, จัดการ permission และ resume session เอกสารทางการยังเตือนด้วยว่าบาง command อาจไม่ได้แสดงสำหรับทุกคน เพราะขึ้นกับ platform, plan และ environment

| คำสั่ง             | ความหมาย                                      | ใช้ตอนไหน                              |
| ------------------ | --------------------------------------------- | -------------------------------------- |
| `/help`            | ดูคำสั่งที่ใช้ได้                             | ใช้ตอนจำ command ไม่ได้                |
| `/init`            | สร้างไฟล์ `CLAUDE.md` เริ่มต้นให้โปรเจกต์     | ใช้ครั้งแรกในโปรเจกต์                  |
| `/memory`          | ดูหรือแก้ memory / instruction ที่ Claude ใช้ | ใช้จัดการบริบทระยะยาว                  |
| `/permissions`     | จัดการสิทธิ์ว่า Claude ทำอะไรได้บ้าง          | ใช้ควบคุมความปลอดภัย                   |
| `/plan`            | เข้า plan mode ให้ Claude วางแผนก่อนแก้โค้ด   | ใช้ก่อนงานใหญ่หรือแก้หลายไฟล์          |
| `/model`           | เปลี่ยน model ที่ใช้งาน                       | ใช้เลือก model ให้เหมาะกับงาน          |
| `/effort`          | ปรับระดับ reasoning effort                    | ใช้เมื่องานซับซ้อนขึ้น                 |
| `/context`         | ดูว่า context ใช้ไปเท่าไร                     | ใช้ตอน session เริ่มยาว                |
| `/compact`         | สรุป conversation เพื่อลด context             | ใช้ตอนคุยนานหรือ context ใกล้เต็ม      |
| `/clear`           | เริ่ม conversation ใหม่แบบ context โล่ง       | ใช้เมื่อเปลี่ยนงานหรือเริ่มหลุดประเด็น |
| `/resume`          | กลับไปทำ session เดิมต่อ                      | ใช้เมื่อต้องการกลับมางานเก่า           |
| `/diff`            | ดูว่า Claude แก้ไฟล์อะไรไปบ้าง                | ใช้ตรวจงานก่อน commit                  |
| `/code-review`     | ให้ Claude review diff ปัจจุบัน               | ใช้ก่อนส่ง PR หรือ commit              |
| `/security-review` | ตรวจความเสี่ยงด้าน security จาก changes       | ใช้กับงาน auth, API, database          |
| `/rewind`          | ย้อน conversation หรือ code ไปจุดก่อนหน้า     | ใช้ตอน Claude แก้ผิดทาง                |
| `/doctor`          | ตรวจปัญหา installation/settings               | ใช้ตอน Claude Code ทำงานผิดปกติ        |
| `/debug`           | เปิด debug log และช่วย troubleshoot           | ใช้ตอนเจอ bug ใน session               |
| `/usage`           | ดู usage, cost หรือ limit                     | ใช้เช็กการใช้งาน                       |
| `/exit`            | ออกจาก Claude Code                            | ใช้จบ session                          |

---

## 3. คำสั่งที่มือใหม่ควรจำก่อน

ถ้าเพิ่งเริ่มใช้ ไม่ต้องจำทั้งหมด ให้จำแค่ชุดนี้ก่อน

### `/init`

ใช้ตอนเริ่มโปรเจกต์ใหม่ เพื่อให้ Claude สร้างไฟล์ `CLAUDE.md` สำหรับเก็บ context ของโปรเจกต์ เช่น build command, test command, coding style และ workflow ของทีม เอกสาร memory ของ Claude Code ระบุว่า `CLAUDE.md` เป็น markdown file ที่ให้ persistent instructions และ Claude จะอ่านตอนเริ่ม session

ตัวอย่าง:

```text
/init
```

เหมาะกับคำถามประมาณนี้:

```text
/init
ช่วยอ่านโปรเจกต์นี้ แล้วสร้าง CLAUDE.md ให้เหมาะกับโปรเจกต์ React + TypeScript
```

---

### `/plan`

ใช้ให้ Claude คิดก่อนลงมือแก้โค้ด

เหมาะกับงานที่มีหลายไฟล์ เช่น

```text
/plan เพิ่มระบบ login ด้วย JWT และ refresh token
```

ข้อดีคือเราจะเห็นแนวทางก่อนว่า Claude จะไปแก้ไฟล์ไหน ทำอะไรบ้าง ลดโอกาสที่ Claude จะรีบแก้มั่ว

---

### `/permissions`

ใช้จัดการว่า Claude ทำอะไรได้บ้าง เช่น อ่านไฟล์ได้ไหม แก้ไฟล์ได้ไหม รัน command ได้ไหม

เหมาะกับมือใหม่มาก เพราะ Claude Code เป็น coding agent ที่สามารถ read file, edit file และ run command ได้ ดังนั้นควรเข้าใจ permission ก่อนปล่อยให้ทำงานอัตโนมัติ

ตัวอย่าง:

```text
/permissions
```

ใช้เปิดหน้าจัดการ permission แล้วเลือกว่าจะ allow / ask / deny อะไร

---

### `/diff`

ใช้ดูว่า Claude แก้ไฟล์อะไรไปบ้าง

ตัวนี้สำคัญมาก เพราะก่อน commit หรือก่อนเชื่อผลลัพธ์ ควรตรวจ diff เสมอ

ตัวอย่าง:

```text
/diff
```

ใช้หลังจาก Claude แก้โค้ดเสร็จ เพื่อเช็กว่าแก้ตรง requirement จริงไหม

---

### `/code-review`

ใช้ให้ Claude review code ที่เพิ่งแก้

ตัวอย่าง:

```text
/code-review
```

หรือถ้าต้องการให้แก้บางจุดอัตโนมัติ:

```text
/code-review --fix
```

เหมาะมากก่อน commit หรือก่อนส่ง pull request

---

### `/context`

ใช้ดูว่า session ตอนนี้ context แน่นแค่ไหน

เมื่อเราให้ Claude อ่านไฟล์เยอะ ๆ คุยนาน ๆ หรือรัน command หลายรอบ context จะเริ่มเต็มและอาจทำให้คุณภาพคำตอบลดลง เอกสาร best practices ของ Claude Code แนะนำให้จัดการ context อย่างจริงจัง โดยใช้ `/clear` ระหว่างงานที่ไม่เกี่ยวกัน และใช้ `/compact <instructions>` เพื่อสรุป conversation ตอน session ยาว

ตัวอย่าง:

```text
/context
```

---

### `/compact`

ใช้สรุป conversation ให้สั้นลง แต่ยังเก็บสาระสำคัญไว้

ตัวอย่าง:

```text
/compact focus on auth flow, modified files, and test commands
```

เหมาะกับ session ที่ทำงานยาวมาก เช่น debug มาหลายรอบ แก้หลายไฟล์ แล้วอยากให้ Claude ยังจำเรื่องสำคัญได้ แต่ลด context ที่ไม่จำเป็น

---

### `/clear`

ใช้เริ่ม context ใหม่

ตัวอย่าง:

```text
/clear
```

ใช้เมื่อเปลี่ยนงาน เช่น เมื่อกี้ทำ login เสร็จแล้ว ต่อไปจะไปทำ dashboard ซึ่งไม่เกี่ยวกันมาก ควร `/clear` เพื่อให้ Claude ไม่แบก context เก่าโดยไม่จำเป็น

---

### `/resume`

ใช้กลับมาทำ session เดิมต่อ

ตัวอย่าง:

```text
/resume
```

หรือจาก Terminal:

```bash
claude -c
```

เหมาะกับงานที่ทำค้างไว้ เช่น เมื่อวาน refactor auth ยังไม่เสร็จ วันนี้กลับมาทำต่อ

---

## 4. Workflow ตัวอย่างสำหรับมือใหม่

### เริ่มโปรเจกต์ใหม่

```bash
cd my-app
claude
```

จากนั้นใน Claude Code:

```text
/init
```

แล้วตามด้วย:

```text
/plan ช่วยวิเคราะห์โครงสร้างโปรเจกต์นี้ และเสนอแนวทางปรับปรุง
```

---

### ให้ Claude แก้ feature ใหม่

```text
/plan เพิ่มหน้า login ด้วย React Hook Form และ validation
```

เมื่อแผนโอเคแล้ว ค่อยให้ Claude ลงมือทำ

หลังทำเสร็จ:

```text
/diff
/code-review
```

---

### Session เริ่มยาวหรือ Claude เริ่มหลุด

```text
/context
```

ถ้า context เยอะ:

```text
/compact focus on current implementation, modified files, known bugs, and next steps
```

ถ้าเปลี่ยนงานใหม่:

```text
/clear
```

---

### Claude แก้ผิดทาง

```text
/rewind
```

ใช้ย้อนกลับไปจุดก่อนหน้า แล้วค่อยเขียน prompt ใหม่ให้ชัดกว่าเดิม

---

## 5. สรุป

มือใหม่ไม่จำเป็นต้องจำทุกคำสั่งของ Claude Code

ให้เริ่มจากชุดนี้ก่อน:

```text
claude
/init
/plan
/permissions
/diff
/code-review
/context
/compact
/clear
/resume
/rewind
```

แนวคิดสำคัญคือ

* ใช้ `/init` เพื่อให้ Claude เข้าใจโปรเจกต์
* ใช้ `/plan` ก่อนแก้งานใหญ่
* ใช้ `/permissions` เพื่อคุมความปลอดภัย
* ใช้ `/diff` และ `/code-review` เพื่อตรวจงาน
* ใช้ `/context`, `/compact`, `/clear` เพื่อจัดการ context
* ใช้ `/resume` เพื่อกลับมางานเดิม
* ใช้ `/rewind` เมื่อ Claude ไปผิดทาง

Claude Code ไม่ใช่แค่ chatbot สำหรับถามตอบโค้ด แต่เป็น coding agent ที่ช่วยอ่านไฟล์ แก้โค้ด รัน command และทำงานร่วมกับโปรเจกต์จริงได้ ดังนั้นยิ่งเราเข้าใจคำสั่งพื้นฐานเหล่านี้มากเท่าไร เราก็จะควบคุม workflow ได้ดีขึ้นเท่านั้น
