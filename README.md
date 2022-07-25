# 🪶 ng-lite starter

> Minimal starter for Angular projects.

See this [dev.to article](WIP) to see how this starter was created and for more details about the differences with Angular CLI's default `ng new`.

## Usage

To create a new project from this starter, you can either:

- Run `npx degit sinedied/ng-lite-starter <project-name>`
- Or select **Use this template** button at the top of this repository and follow the instructions.

## Tasks

This starter is used the same way as any Angular project, ie using the included NPM scripts or the Angular CLI directly:

- `ng serve`: run dev server at `http://localhost:4200/`
- `ng build`: build the project in the `dist/` directory.
- `ng generate component component-name`: generates a new component.

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.

## Add unit testing

You can add unit testing to your project using the [Jest](https://jestjs.io) testing framework by following these steps:

1. Run `npm install --save-dev jest @angular-builders/jest @types/jest`
2. Add a `jest.config.js` file to your project root with the following content:
  ```js
  module.exports = {
    clearMocks: true,
    collectCoverage: true,
    coverageDirectory: "coverage",
  };
  ```
3. Add a `tsconfig.spec.json` file to your project root with the following content:
  ```json
  {
    "extends": "./tsconfig.json",
    "compilerOptions": {
      "outDir": "./out-tsc/spec",
      "types": ["jest"],
      "esModuleInterop": true
    },
    "include": [
      "src/**/*.spec.ts",
      "src/**/*.d.ts"
    ]
  }
  ```
4. In your `angular.json` file, add this after your `serve` configuration (under the `architect` key):
  ```json
  "test": {
    "builder": "@angular-builders/jest:run",
    "options": {
      "tsConfig": "tsconfig.spec.json"
    }
  },
  ```
  If you want to have tests generated by default when using the `ng generate` command, you can also remove all the `"skipTests": true` occurences in this file.
5. Create your first test in `src/app/app.component.spec.ts`:
  ```typescript
  import { ComponentFixture, TestBed } from '@angular/core/testing';
  import { AppComponent } from './app.component';

  describe('AppComponent', () => {
    let component: AppComponent;
    let fixture: ComponentFixture<AppComponent>;

    beforeEach(async () => {
      await TestBed.configureTestingModule({
        imports: [AppComponent],
      }).compileComponents();

      fixture = TestBed.createComponent(AppComponent);
      component = fixture.componentInstance;
      fixture.detectChanges();
    });

    it('should create the component', () => {
      expect(component).toBeTruthy();
    });
  });
  ```

You can now run your test with `ng test` or `ng test --watch`.
