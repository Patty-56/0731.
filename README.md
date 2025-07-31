import pandas as pd

# 讀取主檔與對照表（請自行改路徑）
df_main = pd.read_excel("main.xlsx")        # 原始資料檔
df_lookup = pd.read_excel("lookup.xlsx")    # 有姓名與身分證的對照表

# ✅ 檢查欄位名稱
print("主檔欄位：", df_main.columns.tolist())
print("對照表欄位：", df_lookup.columns.tolist())

# 🧩 合併：用身分證號對應姓名
# 假設欄位為：主檔 "身份證字號"，對照表 "身分證號", "姓名"
merged_df = pd.merge(
    df_main,
    df_lookup[['身分證號', '姓名']],
    left_on='身份證字號',
    right_on='身分證號',
    how='left'
)

# ✅ 可選：刪掉多餘欄位，只保留補好的人名
# merged_df.drop(columns=['身分證號'], inplace=True)

# ✨ 輸出成新 Excel 檔案
merged_df.to_excel("output_對應好姓名的檔案.xlsx", index=False)

print("✅ 合併完成！結果儲存在 'output_對應好姓名的檔案.xlsx'")

