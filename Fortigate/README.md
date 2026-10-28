
# FortiGate Firewall Policy Cleaner & Renumbering Tool

用於 FortiGate 防火牆 Policy 遷移、跨設備匯入或規則整頓時的自動清理工具。

## 解決痛點
在處理 FortiOS 防火牆設定檔（`config firewall policy`）搬遷或整併時，常會遇到兩個問題：
1. **UUID 衝突**：原有規則帶有設備生成的 `set uuid`，直接批次貼入新機器時易報錯或造成狀態混亂。
2. **規則 ID 破碎與衝突**：規則經過長期增刪後 ID 不連續（如 1, 5, 23, 102...），整批匯入容易與目標設備現有 ID 衝撞。

## 主要功能
- **自動剔除 UUID**：過濾並移除所有 `set uuid` 設定行。
- **連續遞增重新編號**：將所有 `edit <id>` 規則依序重新由 `1` 開始連續編號（保持原有縮排結構）。
- **保留原始結構**：除 UUID 與 ID 重新編號外，其餘物件關聯、介面與動作設定均原樣輸出。

## 使用方式

1. 將 FortiGate 的 Policy 配置區段複製並另存為 `policy.txt`。
2. 執行 Python 腳本：
   ```bash
   python renumber_policy.py
