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
         
        \begin{table}[h!t] % 使用 table* 以便跨越双栏
        \vspace{-1em}
        \centering
        \caption{The mAP values of different approaches produced on the CD-FSOD benchmarks in case of 1-shot, 5-shot, and 10-shot. Here ``w/ FT'' and ``w/o FT'' denote the results produced with and without fine-tuning, respectively.}
        % \scriptsize % 调整字体大小
        %\small
        \scriptsize
        % \renewcommand{\arraystretch}{0.9} % 调整行距,之前0.75
        \setlength{\tabcolsep}{0.45pt} % 调整列距，默认值通常是6pt
        % \setlength{\aboverulesep}{10pt} % 规则上方的间隔
    
        \resizebox{0.48\textwidth}{!}{  % 将表格宽度调整为80%的页面宽度
        \begin{tabular}{@{}lcccccccccc@{}}
        % \begin{tabular}{l|c|c|c|c|c|c|c|c}
            \toprule
            % \scalebox{0.9}{Method} & \scalebox{0.9}{Backbone} & \scalebox{0.9}{ArTaxOr} & \scalebox{0.9}{Clipart1k} & \scalebox{0.9}{DIOR} & \scalebox{0.9}{DeepFish} & \scalebox{0.9}{NEU-DET} & \scalebox{0.9}{UODD} & \scalebox{0.9}{Avg.} \\ \midrule
            Method & Backbone & ArTaxOr & Clipart1k & DIOR & DeepFish & NEU-DET & UODD & Avg. \\ \midrule
            % \cmidrule(r){3-9} % partial line under datasets
            \textbf{1-SHOT} & & & & & & & & \\ 
            Meta-RCNN\cite{Meta-RCNN} & ResNet50 & 2.8 & - & 7.8 & - & - & 3.6 & / \\
            TFA w/cos\cite{TFA} & ResNet50 & 3.1 & - & 8.0 & - & - & 4.4 & / \\
            FSCE\cite{FSCE} & ResNet50 & 3.7 & - & 8.6 & - & - & 3.9 & / \\
            DeFRCN\cite{DeFRCN} & ResNet50 & 3.6 & - & 9.3 & - & - & 4.5 & / \\
            Distill-CDFSOD\cite{Distill_cdfsod} & ResNet50 & 5.1 & 7.6 & 10.5 & / & / & 5.9 & / \\
            ViTDeT-FT\cite{ViTDeT} & ViT-B/14 & 5.9 & 6.1 & 12.9 & 0.9 & 2.4 & 4.0 & 5.4 \\
            Detic\cite{Detic} & ViT-L/14 & 0.6 & 11.4 & 0.1 & 0.9 & 0.0 & 0.0 & 2.2 \\
            Detic-FT\cite{Detic} & ViT-L/14 & 3.2 & 15.1 & 4.1 & 9.0 & \textcolor{blue}{3.8} & 4.2 & 6.6 \\
            DE-ViT\cite{DE-ViT} & ViT-L/14 & 0.4 & 0.5 & 2.7 & 0.4 & 0.4 & 1.5 & 1.0 \\  
            DE-ViT-FT\cite{DE-ViT} & ViT-L/14 & 10.5 & 13.0 & 14.7 & 19.3 & 0.6 & 2.4 & 10.1 \\
            CD-ViTO\cite{CD-ViTO} & ViT-L/14 & {21.0} & {17.7} & \textcolor{red}{17.8} & {20.3} & 3.6 & 3.1 & {13.9} \\ 
            \rowcolor{gray!30}  % 设置此行背景为灰色
            {CDFormer w/o FT (ours)} & ViT-L/14 & \textcolor{blue}{29.4} & \textcolor{blue}{49.6} & {8.0} & \textcolor{blue}{27.7} & 3.0 & \textcolor{blue}{12.2} & \textcolor{blue}{21.6} \\ 
            \rowcolor{gray!30}  % 设置此行背景为灰色
            {CDFormer w/FT (ours)} & ViT-L/14 & \textcolor{red}{36.0} & \textcolor{red}{54.0} & \textcolor{blue}{16.3} & \textcolor{red}{34.5} & \textcolor{red}{7.4} & \textcolor{red}{12.7} & \textcolor{red}{26.8} \\
            \midrule
            \textbf{5-SHOT} & & & & & & & & \\
            Meta-RCNN\cite{Meta-RCNN} & ResNet50 & 8.5 & - & 17.7 & - & - & 8.8 & / \\
            TFA w/cos\cite{TFA} & ResNet50 & 8.8 & - & 18.1 & - & - & 8.7 & / \\
            FSCE\cite{FSCE} & ResNet50 & 10.2 & - & 18.7 & - & - & 9.6 & / \\
            DeFRCN\cite{DeFRCN} & ResNet50 & 9.9 & - & 18.9 & - & - & 9.9 & / \\
            Distill-CDFSOD\cite{Distill_cdfsod} & ResNet50 & 12.5 & 23.3 & 19.1 & 15.5 & \textcolor{red}{16.0} & 12.2 & 16.4 \\
            ViTDeT-FT\cite{ViTDeT} & ViT-B/14 & 20.9 & 23.3 & 23.3 & 9.0 & 13.5 & 11.1 & 16.9 \\
            Detic\cite{Detic} & ViT-L/14 & 0.6 & 11.4 & 0.1 & 0.9 & 0.0 & 0.0 & 2.2 \\
            Detic-FT\cite{Detic} & ViT-L/14 & 8.7 & 20.2 & 12.1 & 14.3 & 14.1 & 10.4 & 13.3 \\
            DE-ViT\cite{DE-ViT} & ViT-L/14 & 10.1 & 5.5 & 7.8 & 2.5 & 1.5 & 3.1 & 5.1 \\
            DE-ViT-FT\cite{DE-ViT} & ViT-L/14 & 38.0 & 38.1 & 23.4 & 21.2 & 7.8 & 5.0 & 22.3 \\
            CD-ViTO\cite{CD-ViTO} & ViT-L/14 & \textcolor{blue}{47.9} & {41.1} & \textcolor{blue}{26.9} & {22.3} & 11.4 & 6.8 & \textcolor{blue}{26.1} \\ 
    
            \rowcolor{gray!30}  % 设置此行背景为灰色
            {CDFormer w/o FT (ours)} & ViT-L/14 & {38.4} & \textcolor{blue}{53.6} & {7.9} & \textcolor{blue}{24.6} & 3.6 & \textcolor{blue}{16.5} & {24.1} \\ 
            \rowcolor{gray!30}  % 设置此行背景为灰色
            {CDFormer w/FT (ours)} & ViT-L/14 & \textcolor{red}{65.0} & \textcolor{red}{58.9} & \textcolor{red}{28.1} & \textcolor{red}{31.7} & \textcolor{blue}{15.0} & \textcolor{red}{23.8} & \textcolor{red}{37.1} \\
            \midrule
            \textbf{10-SHOT} & & & & & & & & \\
            Meta-RCNN\cite{Meta-RCNN} & ResNet50 & 14.0 & - & 20.6 & - & - & 11.2 & / \\
            TFA w/cos\cite{TFA} & ResNet50 & 14.8 & - & 20.5 & - & - & 11.8 & / \\
            FSCE\cite{FSCE} & ResNet50 & 15.9 & - & 21.9 & - & - & 12.0 & / \\
            DeFRCN\cite{DeFRCN} & ResNet50 & 15.5 & - & 22.9 & - & - & 12.1 & / \\
            Distill-CDFSOD\cite{Distill_cdfsod} & ResNet50 & 18.1 & 27.3 & 26.5 & 15.5 & \textcolor{red}{21.1} & 14.5 & 20.5 \\
            ViTDeT-FT\cite{ViTDeT} & ViT-B/14 & 23.4 & 25.6 & 29.4 & 6.5 & 15.8 & 15.6 & 19.4 \\
            Detic\cite{Detic} & ViT-L/14 & 0.6 & 11.4 & 0.1 & 0.9 & 0.0 & 0.0 & 2.2 \\
            Detic-FT\cite{Detic} & ViT-L/14 & 12.0 & 22.3 & 15.4 & 17.9 & 16.8 & 14.4 & 16.5 \\
            DE-ViT\cite{DE-ViT} & ViT-L/14 & 9.2 & 11.0 & 8.4 & 2.1 & 1.8 & 3.1 & 5.9 \\
            DE-ViT-FT\cite{DE-ViT} & ViT-L/14 & 49.2 & 40.8 & 25.6 & 21.3 & 8.8 & 5.4 & 25.2 \\
            CD-ViTO\cite{CD-ViTO} & ViT-L/14 & \textcolor{blue}{60.5} & {44.3} & \textcolor{blue}{30.8} & {22.3} & 12.8 & 7.0 & \textcolor{blue}{29.6} \\ 
            
            \rowcolor{gray!30}  % 设置此行背景为灰色
            {CDFormer w/o FT (ours)} & ViT-L/14 & {37.3} & \textcolor{blue}{53.5} & {7.9} & \textcolor{blue}{25.7} & 4.0 & \textcolor{blue}{16.7} & {24.2} \\ 
            \rowcolor{gray!30}  % 设置此行背景为灰色
            {CDFormer w/FT (ours)} & ViT-L/14 & \textcolor{red}{68.7} & \textcolor{red}{59.0} & \textcolor{red}{32.5} & \textcolor{red}{35.5} & \textcolor{blue}{18.1} & \textcolor{red}{26.4} & \textcolor{red}{40.0} \\
            \bottomrule
        \end{tabular}
        }
    \label{all}
    \end{table}

         
          " display-mode />
        </p>

        
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>

</style>
