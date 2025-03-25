<script lang="ts">
import { defineComponent } from 'vue'
import { VueLatex } from 'vatex'

export default defineComponent({
  components: {
    VueLatex
  }
})
</script>

<template>
  <div>
    <el-divider />

    <el-row justify="center">
      <h1 class="section-title">Latex</h1>
    </el-row>

    <el-row justify="center">
      <el-col :xs="24" :sm="20" :md="16" :lg="12" :xl="12">
        <p>
        Thanks to
        <a href="https://katex.org/docs/options.html" target="_blank">KaTex</a>
        and
        <a href="https://github.com/Shimada666/VaTex" target="_blank">VaTex</a>,
        now we can show an inline
        <VueLatex expression="\LaTeX" />
        formula, like
        <VueLatex expression="1+1=2" />.
        And we can show an interline formula like this: 
        <VueLatex expression="
            D(x) = \begin{cases}
            \lim\limits_{x \to 0} \frac{a^x}{b+c}, & x<3 \\
            \pi, & x=3 \\
            \int_a^{3b}x_{ij}+e^2 \mathrm{d}x,& x>3 \\
            \end{cases}
          " display-mode />
        </p>

        <!-- 添加LaTeX表格 -->
        <VueLatex expression="
        \begin{table}[h!t]
          \vspace{-1em}
          \centering
          \caption{The mAP values of different approaches produced on the CD-FSOD benchmarks in case of 1-shot, 5-shot, and 10-shot. Here ``w/ FT'' and ``w/o FT'' denote the results produced with and without fine-tuning, respectively.}
          \scriptsize
          \setlength{\tabcolsep}{0.45pt}
          \resizebox{0.48\textwidth}{!}{
          \begin{tabular}{@{}lcccccccccc@{}}
              \toprule
              Method & Backbone & ArTaxOr & Clipart1k & DIOR & DeepFish & NEU-DET & UODD & Avg. \\ \midrule
              \textbf{1-SHOT} & & & & & & & & \\ 
              Meta-RCNN\cite{Meta-RCNN} & ResNet50 & 2.8 & - & 7.8 & - & - & 3.6 & / \\
              \rowcolor{gray!30}
              {CDFormer w/FT (ours)} & ViT-L/14 & \textcolor{red}{36.0} & \textcolor{red}{54.0} & \textcolor{blue}{16.3} & \textcolor{red}{34.5} & \textcolor{red}{7.4} & \textcolor{red}{12.7} & \textcolor{red}{26.8} \\
              \midrule
              \textbf{5-SHOT} & & & & & & & & \\
              \rowcolor{gray!30}
              {CDFormer w/FT (ours)} & ViT-L/14 & \textcolor{red}{65.0} & \textcolor{red}{58.9} & \textcolor{red}{28.1} & \textcolor{red}{31.7} & \textcolor{blue}{15.0} & \textcolor{red}{23.8} & \textcolor{red}{37.1} \\
              \midrule
              \textbf{10-SHOT} & & & & & & & & \\
              \rowcolor{gray!30}
              {CDFormer w/FT (ours)} & ViT-L/14 & \textcolor{red}{68.7} & \textcolor{red}{59.0} & \textcolor{red}{32.5} & \textcolor{red}{35.5} & \textcolor{blue}{18.1} & \textcolor{red}{26.4} & \textcolor{red}{40.0} \\
              \bottomrule
          \end{tabular}
          }
          \label{all}
        \end{table}
        " display-mode />   
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>

</style>
