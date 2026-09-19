# Module Inheritance Routing (Claude Code)

Khi user yêu cầu kế thừa module từ Steal A Pet vào SharedLibs, hoặc từ SharedLibs
sang project khác, dùng Skill tool với các skill sau (đã đăng ký ở .claude/skills/):

- `source-to-shared-router` — khi: "kế thừa/inherit [module] từ Steal A Pet vào SharedLibs"
- `shared-to-consumer-router` — khi: "thêm/kế thừa module [module] từ SharedLibs vào [project]"
- `review-inherited-module` — dùng kèm 2 router trên, tự chọn section theo checklist trong skill

Quy ước đặt tên module skill: `[module]-source-to-shared`, `[module]-shared-to-consumer`.
User không cần gọi tên skill tường minh — mô tả tự nhiên là đủ.

## Force keyword

Nếu prompt chứa "force" / "làm luôn" / "không cần plan": bỏ qua bước lập Phase Plan,
chạy thẳng (vẫn chạy Complexity Gate để ghi log).
Mặc định (không có từ khoá): LUÔN đề xuất Phase Plan nếu module bị đánh giá phức tạp
(xem `.agent/skills/shared-to-consumer-router/SKILL.md` mục Complexity Gate), dừng
lại chờ user duyệt từng phase — dùng `ExitPlanMode` khi khả dụng.

Xem đầy đủ: `.agent/INDEX.md`
