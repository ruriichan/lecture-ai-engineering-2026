# 第3回 解答

## 演習

- 第1回（素のLLM）とエージェントの回答の違い：素のLLMは自分の知識をもとに回答するが、エージェントは必要に応じてツールを呼び出し、用語集や講義資料を確認して回答する。
- `--trace` で見えたツール呼び出し（ツール名と引数）：
search_glossary({'query': 'LoRA'})
search_glossary({'query': 'QLoRA'})
make_quiz({'lecture': 2})
get_lecture_summary({'lecture': 2})
- 1つの質問での LLM 呼び出し回数（`requests`）：LoRAとQLoRAの質問では2回、確認問題の質問では2回。
- 追加したツールと、docstring に書いた説明：make_quiz(lecture) を追加した。
指定した回の用語集から用語を1つ選び、確認問題と答えを作るツール。

## 宿題

- 取り組んだレベル：基礎
- やったこと：app/agent.py の INSTRUCTIONS を変更し、利用者が求めた場合は宿題の答えも説明してよいという指示にした。
- 結果：第2回の宿題の答えを質問したところ、講義概要を取得する get_lecture_summary が呼び出された。宿題の具体的な設問が不明だったため、エージェントは設問を尋ねた。

(aie2026-exercises) @ruriichan ➜ /workspaces/lecture-ai-engineering-2026 (lec03) $ uv run python -m app.agent --trace "第2回の宿題の答えを教えて"
[model] gemini-3.5-flash-lite
第2回では、事前学習とファインチューニングの違い、LoRAによる効率的な学習、演習でのFAQデータを使ったSFT（教師ありファインチューニング）などを学びます。

講座（AIE2026）の第2回における宿題の具体的な設問や課題について教えていただけますでしょうか？ 課題の内容に合わせて、回答や解説をご案内いたします。

（関連する回：第2回）

--- trace ---
[tool call]   get_lecture_summary({'lecture': 2})
[tool return] get_lecture_summary -> # 第2回 ファインチューニングとLoRA

## この回のねらい

- 事前学習とファインチューニングの違い、ファインチューニングが向く場面と向かない場面を理解する
- LoRAの考え方を理解し、Google Colab上で小さなモデルを…
[usage] RunUsage(cost=Decimal('0.0006725'), details={'text_prompt_tokens': 1350}, input_text_tokens=1350, input_tokens=1350, output_tokens=107, requests=2, tool_calls=1)

- 気づき・疑問：エージェントの回答は、設定した指示だけでなく、質問内容や利用できるツールにも影響されることが分かった。
