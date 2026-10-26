# La Paz — Tech notes

> ข้อมูล ณ ต.ค. 2026 — ราคาและโควตาเปลี่ยนบ่อย เช็คหน้า pricing ทางการอีกครั้งก่อนตัดสินใจ

## Stack

- **Next.js + Supabase** (ตัดสินใจแล้ว)
- SvelteKit ถูกพิจารณาแล้วไม่เลือก: ทำคนเดียวกับ AI ใช้ React/Next.js ดีกว่า เพราะ AI เขียนได้แม่นกว่า ไลบรารี UI เยอะกว่า และ Svelte 5 เปลี่ยน syntax (runes) ทำให้ AI มักเขียนแบบเก่าปนมา

## Vercel Hobby (ฟรี)

- **ข้อจำกัดหลักคือเงื่อนไขการใช้งาน ไม่ใช่โควตา**: Hobby ใช้ได้เฉพาะงานส่วนตัวที่ไม่ใช่เชิงพาณิชย์ แอปที่ใช้ทำงานของร้านมีแนวโน้มนับเป็นเชิงพาณิชย์ ถ้าไม่แน่ใจ Vercel ให้ติดต่อ Support
- Pro = $20/เดือน
- ทางเลือก: ทำแอปเป็น static export (PWA ฝั่ง client คุยกับ Supabase ตรง) แล้วโฮสต์ static ฟรีที่อื่น (เช่น Cloudflare Pages) — ต้องเช็คเงื่อนไขของผู้ให้บริการนั้นอีกครั้ง
- ช่วงพัฒนา/ทดลอง ใช้ Hobby ได้ ตัดสินใจเรื่องโฮสต์ตอนจะใช้งานจริง

## Supabase Free

- DB 500 MB — พอสำหรับร้านเดียวหลายปี (ข้อมูลเป็นตัวอักษร)
- File storage 1 GB — ต้องย่อรูป (ของเสีย / รูป reference / ใบเสร็จ) ฝั่ง client ก่อนอัปโหลด
- Egress ~5 GB/เดือน
- **Pause หลังไม่มีการใช้งาน 7 วัน** — ตอนร้านใช้ทุกวันไม่มีปัญหา แต่ช่วงพัฒนาอาจโดน pause
- **ไม่มี backup อัตโนมัติ** (daily backup เป็นของ Pro $25/เดือน) — ข้อมูลยอดขาย/เงินต้องมี backup เอง เช่น `pg_dump` รายวันด้วย GitHub Actions หรืออัปเกรดเป็น Pro ตอนใช้งานจริง
- **Breaking change (Data API grants)**: project ใหม่ตั้งแต่ 30 พ.ค. 2026 และ project เดิมตั้งแต่ 30 ต.ค. 2026 — ตารางใหม่ใน `public` จะไม่เปิดให้ supabase-js / REST เข้าถึงจนกว่าจะ `GRANT` สิทธิ์ให้ role (`anon`, `authenticated`, `service_role`) เอง ต้องใส่ GRANT ใน migration ทุกตาราง คู่กับ RLS

## Sources

- https://vercel.com/docs/limits/fair-use-guidelines
- https://supabase.com/changelog/45329-breaking-change-tables-not-exposed-to-data-and-graphql-api-automatically
- https://automationatlas.io/answers/supabase-free-tier-limits-2026/
