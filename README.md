    import { Component, OnInit, Input, EventEmitter, Output, ChangeDetectionStrategy, SimpleChanges } from '@angular/core';
    import { FormGroup, FormBuilder, Validators } from '@angular/forms';

    @Component({
      selector: 'app-form-details',
      templateUrl: './form-details.component.html',
      styleUrls: ['./form-details.component.css']
    })
    export class FormDetailsComponent  {

      detailsForm: FormGroup;
      loader: boolean;
      @Input() editCritere: Critere;


      constructor(private _fb: FormBuilder) { 
      this._createForm(); 
      }


      ngOnChanges(changes: SimpleChanges) {
        // changes.prop contains the old and the new value...

        if (changes.editCritere){
          this.editCritere = changes.editCritere.currentValue

          this.detailsForm.controls.name.setValue(this.editCritere.name)
        }


      }

      /**
       * create our reactive form here
       */
      private _createForm() {


          this.detailsForm = this._fb.group({
            name: ['', Validators.required]
          });


      }

      /**
       * submit new form
       */

      onSubmit() {
        const param = this.detailsForm.value;

        console.log(param)


      }
    }



IN YOUR PARENT COMPONENT YOU CAN CALL YOUR COMPONENT WITH editCritere PARAMETER
       
       
       <app-form-details [editCritere]="editCritere" ></app-form-details>

  
