<template>
  <div class="wrapper fill-height" ref="wrapperDiv">
    <canvas width="100%" height="100" ref="canvas"></canvas>
  </div>
</template>

<script lang="ts">
import fs from "fs";
import http from "http";
import { remote, BrowserWindow } from "electron";
import { Vue, Component, Ref } from "vue-property-decorator";
import { fabric } from "fabric";

@Component({})
export default class Canvas extends Vue {
  @Ref() readonly wrapperDiv!: HTMLDivElement;
  @Ref() readonly canvas!: HTMLCanvasElement;

  fabricCanvas: fabric.Canvas | null = null;

  width = 0;
  height = 0;

  resizeFlag = false;

  mounted(): void {
    setTimeout(() => {
      this.init();
      this.drawCanvas();
    }, 100);
    window.onresize = () => {
      if (!this.resizeFlag) {
        this.resizeFlag = true;
        setTimeout(() => {
          this.init();
          this.drawCanvas();
          this.resizeFlag = false;
        }, 600);
      }
    };
  }

  init(): void {
    [this.width, this.height] = [
      this.wrapperDiv.clientWidth,
      this.wrapperDiv.clientHeight
    ];
    const canvas = new fabric.Canvas(this.canvas, {
      preserveObjectStacking: true
    });
    canvas.allowTouchScrolling = true;
    canvas.setWidth(this.width);
    canvas.setHeight(this.height);
    this.fabricCanvas = canvas;
  }

  drawCanvas(): void {
    const canvas = this.fabricCanvas;
    if (canvas == null) return;
    canvas.clear();
    this.drawGrid(canvas);
    this.drawRect(canvas);

    // move
    canvas.on("mouse:move", (opt: any) => {
      this.handleMouseMove(canvas, opt);
    });
  }

  drawRect(canvas: fabric.Canvas): void {
    const rect = new fabric.Rect({
      width: 100,
      height: 100,
      left: 10,
      top: 20,
      fill: "rgba(0,0,0,0)",
      strokeWidth: 1,
      stroke: "red",
      selectable: false,
      evented: false,
      visible: true
    });
    canvas.add(rect);
  }

  drawGrid(canvas: fabric.Canvas): void {
    const gap = 10;
    for (let i = 0; i * gap < this.height; i++) {
      const line = new fabric.Line([0, gap * i, this.width, gap * i], {
        fill: "#eee",
        stroke: "#eee",
        strokeWidth: 1,
        selectable: false,
        evented: false
      });
      canvas.add(line);
    }
    for (let i = 0; i * gap < this.width; i++) {
      const line = new fabric.Line([gap * i, 0, gap * i, this.height], {
        fill: "#eee",
        stroke: "#eee",
        strokeWidth: 1,
        selectable: false,
        evented: false
      });
      canvas.add(line);
    }
  }

  handleMouseMove(canvas: fabric.Canvas, opt: any): void {
    // TODO
    const delta = 2;
  }

  exportPhoto(): void {
    if (this.fabricCanvas) {
      const href = this.fabricCanvas.toDataURL({ format: "png" });
      console.log(href);
      const base64Data = href.replace(/^data:image\/png;base64,/, "");
      // fs.writeFile("/Users/fantingsheng/Desktop/img.png", base64Data, "base64");
      // remote.dialog.showOpenDialog({});
      window.open(href);
      // const file = fs.createWriteStream("pic.png");
      // fs.writeFile("/", href, function(err) {
      //   console.log(err);
      // });
      // http.get(href, function(response) {
      //   response.pipe(file);
      // });
    }
    console.log("export photo");
  }
}
</script>
