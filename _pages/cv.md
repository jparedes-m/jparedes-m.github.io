---
layout: page
title: CV
nav: true
nav_order: 3
permalink: /cv/
---

<p><a href="/assets/pdf/cv.pdf" target="_blank">Download PDF</a></p>

<style>
  #cv-mobile { display: none; }
  #cv-mobile canvas { width: 100%; margin-bottom: 12px; box-shadow: 0 0 4px rgba(0,0,0,.2); }
  @media (max-width: 768px) { #cv-desktop { display: none; } #cv-mobile { display: block; } }
</style>

<iframe id="cv-desktop" src="/assets/pdf/cv.pdf" width="100%" height="800px" style="border:none;"></iframe>
<div id="cv-mobile"></div>

<script src="https://cdn.jsdelivr.net/npm/pdfjs-dist@3.11.174/build/pdf.min.js"></script>
<script>
  if (window.matchMedia("(max-width: 768px)").matches) { // render only on mobile
    pdfjsLib.GlobalWorkerOptions.workerSrc = "https://cdn.jsdelivr.net/npm/pdfjs-dist@3.11.174/build/pdf.worker.min.js";
    pdfjsLib.getDocument("/assets/pdf/cv.pdf").promise.then(async (pdf) => {
      const box = document.getElementById("cv-mobile");
      for (let i = 1; i <= pdf.numPages; i++) {
        const page = await pdf.getPage(i);
        const scale = (box.clientWidth / page.getViewport({ scale: 1 }).width) * (window.devicePixelRatio || 1); // sharp on retina
        const vp = page.getViewport({ scale });
        const c = document.createElement("canvas");
        c.width = vp.width; c.height = vp.height;
        box.appendChild(c);
        await page.render({ canvasContext: c.getContext("2d"), viewport: vp }).promise;
      }
    });
  }
</script>
